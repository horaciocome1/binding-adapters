# binding-adapters
Set of useful binding adapters for databinding component on android. Please fork and add some other useful cases to this index.

## Loading an image
### Adapter
```kotlin
@BindingAdapter("url", "uri", "resourceId", requireAll = false)
@JvmStatic
fun ImageView.loadImage(url: String?, uri: Uri?, resourceId: Int?) {
    val image = if (uri != null && uri != Uri.EMPTY)
        uri
    else
        resourceId ?: url
    Glide.with(context)
        .load(image)
        .transition(DrawableTransitionOptions.withCrossFade())
        .into(this)
}
```
### Layout
```xml
<ImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:url="@{account.icon}" />
```
OR
```xml
<ImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:uri="@{imageUri}" />
```
OR
```xml
<ImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:resourceId="@{@drawable/my_drawable}" />
```

# Loading an list
Note that you can pass an `LiveData` list, since data binding can receive `lifecycleOwner`.
### Adapter
```kotlin
@BindingAdapter("users", "products", requireAll = false)
@JvmStatic
fun RecyclerView.loadList(
    users: LiveData<List<User>>?,
    products: LiveData<List<Product>>?
) {
    if (users != null && users.value != null) {
        layoutManager = LinearLayoutManager(context)
        adapter = UsersAdapter(users.value!!)
    }
    if (products != null && products.value != null) {
        layoutManager = LinearLayoutManager(context)
        adapter = ProductsAdapter(products.value!!)
    }
}
```
### xml
```xml
<androidx.recyclerview.widget.RecyclerView
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      app:reviews="@{liveDataListOfUsers}" /> // or of products
```


## Licences
Copyright 2019 Horácio Flávio Comé Júnior

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations
under the License.
