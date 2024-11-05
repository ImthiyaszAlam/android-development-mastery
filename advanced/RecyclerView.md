# RecyclerView

## Overview

`RecyclerView` is a flexible and efficient widget for displaying large datasets in a scrollable list. It is a part of the AndroidX library and is designed to be more efficient and flexible compared to its predecessor, `ListView`.

## Prebuilt Classes

### 1. **RecyclerView**
- **Description:** The main class used to display the list of items.
- **Usage:** You need to add a `RecyclerView` to your layout and set up an adapter to provide the data.

### 2. **RecyclerView.Adapter**
- **Description:** Abstract class responsible for creating ViewHolders and binding data to them.
- **Usage:** Implement this class to provide the data for your RecyclerView.
- **Code Example:**
  ```java
  public class MyAdapter extends RecyclerView.Adapter<MyAdapter.ViewHolder> {
      private List<String> mData;

      public MyAdapter(List<String> data) {
          this.mData = data;
      }

      @Override
      public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
          View view = LayoutInflater.from(parent.getContext())
                      .inflate(R.layout.item_layout, parent, false);
          return new ViewHolder(view);
      }

      @Override
      public void onBindViewHolder(ViewHolder holder, int position) {
          holder.textView.setText(mData.get(position));
      }

      @Override
      public int getItemCount() {
          return mData.size();
      }

      public static class ViewHolder extends RecyclerView.ViewHolder {
          TextView textView;
          public ViewHolder(View itemView) {
              super(itemView);
              textView = itemView.findViewById(R.id.text_view);
          }
      }
  }
  ```

### 3. **RecyclerView.ViewHolder**
- **Description:** Holds references to the views for each item in the list.
- **Usage:** Extend this class to create custom ViewHolders for your adapter.
- **Code Example:** See above in the `MyAdapter` class.

### 4. **RecyclerView.LayoutManager**
- **Description:** Manages the layout of the RecyclerView's items.
- **Usage:** Choose a LayoutManager based on how you want to arrange your items (e.g., linear, grid).
- **Code Example:**
  ```java
  RecyclerView.LayoutManager layoutManager = new LinearLayoutManager(context);
  recyclerView.setLayoutManager(layoutManager);
  ```

### 5. **RecyclerView.ItemDecoration**
- **Description:** Used to add special drawing and layout offsets to items in the RecyclerView.
- **Usage:** Extend this class to add custom decorations such as dividers or margins.
- **Code Example:**
  ```java
  public class DividerItemDecoration extends RecyclerView.ItemDecoration {
      @Override
      public void onDraw(Canvas c, RecyclerView parent, RecyclerView.State state) {
          super.onDraw(c, parent, state);
          // Custom drawing code here
      }
  }
  ```

### 6. **RecyclerView.ItemAnimator**
- **Description:** Handles animations for changes in items in the RecyclerView.
- **Usage:** Use predefined animations or create custom ones.
- **Code Example:**
  ```java
  recyclerView.setItemAnimator(new DefaultItemAnimator());
  ```

## Key Methods

### **RecyclerView.setAdapter()**
- **Description:** Sets the adapter that provides data to the RecyclerView.
- **Usage:** Call this method to bind your adapter to the RecyclerView.
- **Code Example:**
  ```java
  recyclerView.setAdapter(new MyAdapter(dataList));
  ```

### **RecyclerView.setLayoutManager()**
- **Description:** Sets the LayoutManager that will be used to position the items.
- **Usage:** Call this method to specify how the items will be laid out (e.g., linear or grid).
- **Code Example:**
  ```java
  recyclerView.setLayoutManager(new GridLayoutManager(context, 2));
  ```

## Real-Life Examples

1. **News Feed:** Displaying a list of news articles where each item includes an image, title, and summary.
2. **Contacts List:** Showing a list of contact names with phone numbers in a scrollable list.
3. **Product Catalog:** Displaying a grid of products in an e-commerce app where each item shows a product image and price.

## Summary

RecyclerView is a powerful tool for displaying and managing large sets of data in Android applications. Its flexibility allows you to create various types of lists and grids efficiently.

