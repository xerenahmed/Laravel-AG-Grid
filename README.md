# Laravel AG Grid

Example code:
```php
Route::post('messages', function(Request $request) {
	$builder = Message::leftJoin('posts', 'posts.id', '=', 'messages.post_id')
			->leftJoin('users', 'users.id', '=', 'messages.user_id');
	return AGGridDataBuilder::create($builder)
		->debug(true)
		->defaultSelects([
			'messages.id',
			'messages.message',
			'posts.title',
			'users.name',
		])
		 ->build($request)
		 ->asResponse();
});

Route::get('messages/{field}', function(Request $request, $field) {
	return DB::table('messages')->select($field)->distinct()->orderBy($field, 'asc')->pluck($field);
});
```

AG Grid:
```js
const gridOptions = {
    columnDefs: [
        { field: "id", filter: "agNumberColumnFilter" },
        { field: "message", filter: "agTextColumnFilter" },
        { field: "posts.title", headerName: "Post", filter: "agTextColumnFilter" },
		{ 
            field: "users.name",
            headerName: "User", 
            filter: "agTextColumnFilter",
            searchable: true,
        }
 },

```
