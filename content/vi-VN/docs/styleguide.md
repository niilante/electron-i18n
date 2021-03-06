# Tài liệu về Styleguide của Electron

Đây là những nguyên tắc để viết tài liệu Electron.

## Tiêu đề

* Mỗi trang chỉ có một tiêu đề ở cấp `#` và được viết ngay đầu trang.
* Các tiêu đề của các chương trong cùng một trang phải có cấp độ `##`.
* Chương nhỏ cần được tăng số lượng của `#` theo chiều sâu mà nó nằm so với chương chứa nó.
* Tất cả các từ trong tiêu đề của trang phải được viết hoa, ngoại trừ các liên từ như "của" và "và".
* Chỉ từ đầu tiên của một tiêu đề chương phải được viết hoa.

Lấy `Quick Start` để làm ví dụ:

```markdown
# Quick Start

...

## Main process

...

## Renderer process

...

## Run your app

...

### Run as a distribution

...

### Manually downloaded Electron binary

...
```

Cũng được dùng cho các tài liệu của API, không có ngoại lệ.

## Quy tắc sử dụng Markdown

* Sử dụng `bash` thay thế cho `cmd` trong code (cú pháp của markdown).
* Một dòng nên chứa tối đa 80 kí tự kể cả khoảng cách.
* Phân cấp tiêu đề không được quá 2 cấp (vì markdown sẽ không render quá 2 cấp).
* Tất cả code `js` và `javascript` nên được linted với [tiêu chuẩn của markdown](http://npm.im/standard-markdown).

## Chọn từ

* Sử dụng "will" thay vì "would" khi mô tả các kết quả.
* Sử dụng "in the ___ process" thay vì "on".

## Tài liệu tham khảo về API

Các quy định sau đây chỉ áp dụng cho các tài liệu API.

### Tiêu đề Trang

Each page must use the actual object name returned by `require('electron')` as the title, such as `BrowserWindow`, `autoUpdater`, and `session`.

Under the page tile must be a one-line description starting with `>`.

Sử dụng `session` như một ví dụ:

```markdown
# session

> Manage browser sessions, cookies, cache, proxy settings, etc.
```

### Các module phương thức và sự kiện

For modules that are not classes, their methods and events must be listed under the `## Methods` and `## Events` chapters.

Ví dụ như `autoUpdater` là một ví dụ:

```markdown
# autoUpdater

## Events

### Event: 'error'

## Methods

### `autoUpdater.setFeedURL(url[, requestHeaders])`
```

### Các class

* API classes or classes that are part of modules must be listed under a `## Class: TheClassName` chapter.
* One page can have multiple classes.
* Constructors must be listed with `###`-level titles.
* [Static Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static) must be listed under a `### Static Methods` chapter.
* [Instance Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes#Prototype_methods) must be listed under an `### Instance Methods` chapter.
* Tất cả phương thức có trả về giá trị phải được bắt đầu bằng đoạn mô tả: "Returns `[TYPE]` - Return description" 
  * If the method returns an `Object`, its structure can be specified using a colon followed by a newline then an unordered list of properties in the same style as function parameters.
* Instance Events must be listed under an `### Instance Events` chapter.
* Instance Properties must be listed under an `### Instance Properties` chapter. 
  * Instance properties must start with "A [Property Type] ..."

Sử dụng tài liệu của các class `Session` và `Cookies` làm ví dụ:

```markdown
# session

## Methods

### session.fromPartition(partition)

## Properties

### session.defaultSession

## Class: Session

### Instance Events

#### Event: 'will-download'

### Instance Methods

#### `ses.getCacheSize(callback)`

### Instance Properties

#### `ses.cookies`

## Class: Cookies

### Instance Methods

#### `cookies.get(filter, callback)`
```

### Các phương thức

Chương viết về các phương thức phải viết trong các hình thức sau đây:

```markdown
### `objectName.methodName(required[, optional]))`

* `required` String - A parameter description.
* `optional` Integer (optional) - Another parameter description.

...
```

The title can be `###` or `####`-levels depending on whether it is a method of a module or a class.

For modules, the `objectName` is the module's name. For classes, it must be the name of the instance of the class, and must not be the same as the module's name.

For example, the methods of the `Session` class under the `session` module must use `ses` as the `objectName`.

The optional arguments are notated by square brackets `[]` surrounding the optional argument as well as the comma required if this optional argument follows another argument:

    required[, optional]
    

Below the method is more detailed information on each of the arguments. The type of argument is notated by either the common types:

* [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
* [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
* [`Object`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
* [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
* [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
* Hoặc một loại tùy chỉnh như của Electron: [`WebContent`](api/web-contents.md)

If an argument or a method is unique to certain platforms, those platforms are denoted using a space-delimited italicized list following the datatype. Values can be `macOS`, `Windows`, or `Linux`.

```markdown
* `animate` Boolean (optional) _macOS_ _Windows_ - Animate the thing.
```

`Array` type arguments must specify what elements the array may include in the description below.

The description for `Function` type arguments should make it clear how it may be called and list the types of the parameters that will be passed to it.

### Các sự kiện

Các chương về các sự kiện phải được viết theo kiểu dưới đây:

```markdown
### Event: 'wake-up'

Returns:

* `time` String

...
```

Tiêu đề có thể ở các mức độ `###` hoặc `####`. Cho dù nó là thuộc tính của một module hay của một class.

The arguments of an event follow the same rules as methods.

### Các thuộc tính

Các chương của thuộc tính phải theo quy tắc:

```markdown
### session.defaultSession

...
```

Tiêu đề có thể ở các mức độ `###` hoặc `####`. Cho dù nó là thuộc tính của một module hay của một class.

## Các bản dịch của tài liệu

Các bản dịch của tài liệu Electron nằm trong thư mục `docs-translations`.

Để thêm một thiết lập (hoặc một phần):

* Tạo một thư mục con đặt tên theo tên viết tắt của ngôn ngữ.
* Dịch các tập tin.
* Cập nhật các link tới các tập tin mà bạn đã dịch vào `README.md` nằm trong thư mục ngôn ngữ của bạn.
* Thêm liên kết của thư mục ngôn ngữ đó của bạn vào trang [README](https://github.com/electron/electron#documentation-translations) chính của Electron.

Lưu ý rằng các file trong `docs-translations` chỉ bao gồm những bản dịch, những bản gốc tiếng Anh không xuất phát từ đó.