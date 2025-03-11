

# Paging 3 (Android - Kotlin)

## 📌 What is Paging 3?
Paging 3 is a Jetpack library that helps load and display large data sets efficiently in Android applications. It ensures smooth scrolling and optimizes memory and network usage by loading only the necessary data.

## 📌 Why Use Paging 3?
- **Performance Optimization:** Avoids loading an entire dataset at once, reducing memory usage.
- **Efficient Network Requests:** Loads data in chunks, minimizing API calls.
- **Seamless Pagination:** Handles page state, errors, and refresh operations automatically.
- **Supports Local & Remote Data Sources:** Works well with Room Database, APIs, or both.
- **Built-in Kotlin Coroutines & Flow Support:** Enables reactive and asynchronous data loading.

---

## 📌 How Paging 3 Works?
Paging 3 follows an architecture based on the **Repository Pattern** and consists of the following key components:

1. **PagingSource** - Fetches data from local or remote sources.
2. **Pager** - Connects `PagingSource` and `PagingData`.
3. **PagingData** - Represents paginated data.
4. **PagingDataAdapter** - Efficiently updates UI.
5. **RemoteMediator (optional)** - Supports caching and offline mode.

---

## 📌 Prebuilt Classes and Interfaces in Paging 3

| Component | Description | Example |
|-----------|-------------|---------|
| `PagingSource<Key, Value>` | Retrieves paged data, supports both local & remote sources. | `UserPagingSource : PagingSource<Int, User>()` |
| `PagingData<Value>` | Holds paginated data and can be collected using Kotlin Flow. | `flow<PagingData<User>>` |
| `Pager<Key, Value>` | Creates a flow of `PagingData` from `PagingSource` or `RemoteMediator`. | `Pager(config, pagingSourceFactory).flow` |
| `PagingDataAdapter<Value, ViewHolder>` | Loads paginated data efficiently in `RecyclerView`. | `UserPagingAdapter()` |
| `RemoteMediator<Key, Value>` | Handles offline caching and API + Room integration. | `UserRemoteMediator()` |
| `LoadState` | Represents the state of a page load (Loading, Error, Success). | `LoadState.Loading` |
| `LoadStateAdapter` | Handles UI for loading states in `RecyclerView`. | `UserLoadStateAdapter()` |

---

## 📌 Implementation Guide

### 1️⃣ **Add Dependencies**
```kotlin
dependencies {
    implementation("androidx.paging:paging-runtime-ktx:3.1.1")  // Core Paging 3
}
```

### 2️⃣ **Create a PagingSource**
`PagingSource` fetches data page by page.
```kotlin
class UserPagingSource(private val apiService: ApiService) : PagingSource<Int, User>() {
    override suspend fun load(params: LoadParams<Int>): LoadResult<Int, User> {
        return try {
            val page = params.key ?: 1
            val response = apiService.getUsers(page, params.loadSize)
            LoadResult.Page(
                data = response.users,
                prevKey = if (page == 1) null else page - 1,
                nextKey = if (response.users.isEmpty()) null else page + 1
            )
        } catch (e: Exception) {
            LoadResult.Error(e)
        }
    }
}
```

### 3️⃣ **Use Pager to Create PagingData Flow**
```kotlin
class UserRepository(private val apiService: ApiService) {
    fun getUsers(): Flow<PagingData<User>> {
        return Pager(
            config = PagingConfig(pageSize = 20, enablePlaceholders = false),
            pagingSourceFactory = { UserPagingSource(apiService) }
        ).flow
    }
}
```

### 4️⃣ **Set Up ViewModel**
```kotlin
class UserViewModel(private val repository: UserRepository) : ViewModel() {
    val userPagingData: Flow<PagingData<User>> = repository.getUsers()
        .cachedIn(viewModelScope)
}
```

### 5️⃣ **Create PagingDataAdapter**
```kotlin
class UserPagingAdapter : PagingDataAdapter<User, UserViewHolder>(UserDiffCallback()) {
    override fun onBindViewHolder(holder: UserViewHolder, position: Int) {
        val user = getItem(position)
        holder.bind(user)
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): UserViewHolder {
        val view = LayoutInflater.from(parent.context).inflate(R.layout.item_user, parent, false)
        return UserViewHolder(view)
    }
}
```

### 6️⃣ **Connect Everything in Activity/Fragment**
```kotlin
class UserFragment : Fragment() {
    private val viewModel: UserViewModel by viewModels()
    private lateinit var adapter: UserPagingAdapter

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        adapter = UserPagingAdapter()
        recyclerView.adapter = adapter.withLoadStateFooter(LoadStateAdapter { adapter.retry() })

        lifecycleScope.launch {
            viewModel.userPagingData.collectLatest { pagingData ->
                adapter.submitData(pagingData)
            }
        }
    }
}
```

---

## 📌 Types of Pagination in Paging 3

### **1. Network-Only Pagination (Remote Paging)**
- Fetches data from API directly.
- Uses `PagingSource` only.
- Suitable for APIs that return paginated responses.

**Example:** Fetching users from a REST API.

### **2. Database-Only Pagination (Local Paging)**
- Fetches data from local storage (e.g., Room).
- Uses `PagingSource` with `Room`.
- Suitable for large offline datasets.

**Example:** Loading a local list of contacts.

### **3. Network + Local Pagination (RemoteMediator)**
- Combines API with Room Database for caching.
- Uses `RemoteMediator` to sync data between API & local database.
- Suitable for apps requiring offline support.

**Example:** News app fetching articles from API and storing them in Room.

---

## 📌 Differences Between Paging 2 & Paging 3

| Feature | Paging 2 | Paging 3 |
|---------|---------|---------|
| API | Uses `DataSource` & `LiveData` | Uses `PagingSource` & `Flow` |
| Coroutines Support | Not supported | Fully supported |
| Network + Local | Difficult to implement | `RemoteMediator` makes it easy |
| Performance | Requires manual optimizations | More optimized & efficient |

---

## 📌 Real-Life Example: News App
A news app using Paging 3:
1. Fetches news articles from an API.
2. Stores data in Room for offline support.
3. Uses `RemoteMediator` to sync API & local database.

---

## 📌 Summary
✔ Paging 3 efficiently handles large datasets.  
✔ Supports **Network**, **Local**, and **Hybrid (Network + Local)** paging.  
✔ Fully integrates with **Coroutines, Flow, LiveData**, and **Room Database**.  
✔ Provides **automatic handling of errors & UI states**.
