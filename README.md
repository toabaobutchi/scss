# SCSS

> [!Important]
>
> Tài liệu chỉ mang tính tham khảo và tổng hợp các trường hợp sử dụng thường gặp. Các trường hợp nâng cao khác hãy tìm tại [trang chủ của SASS](https://sass-lang.com/).

## Cài đặt

### # Ứng dụng HTML trong Visual Studio Code

Nếu sử dụng cho ứng dụng web đơn giản với HTML, ta có thể cài đặt extension [**Live Sass Compiler**](https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass) trong Visual Studio Code. 

Sau khi cài đặt, tạo file **`.scss`** và bắt đầu viết mã. Chức năng **Watch Sass** (tìm thấy ở thanh trạng thái - mặc định nằm bên dưới IDE) sẽ biên dịch SCSS thành CSS và ta có thể sử dụng file CSS này trong các file HTML.

<img src="https://github.com/toabaobutchi/scss/assets/147165208/4b940402-0a2d-4ed3-b337-78db7d938f9a" width="500px" />

### # Cài đặt thông qua NPM

> [!Important]
>
> Để sử dụng [**npm**](https://www.npmjs.com/), bắt buộc máy đã tải [**Node.js**](https://nodejs.org/en)

- Lệnh tải SCSS bằng NPM:

```
npm i -g sass
```

- Biên dịch `.scss` thành `.css`:

```
sass <source>.scss <des>.css
```

Trong đó, **`<source>`** là đường dẫn đến file `.scss` muốn biên dịch. **`<des>`** là đường dẫn của file `.css` sẽ biên dịch (đường dẫn đích có thể chưa tồn tại).

**Ví dụ:**

```
sass source/stylesheets/index.scss build/stylesheets/index.css
```

> [!Tip]
>
> - Trong trường hợp muốn biên dịch toàn bộ file `.scss` thành các file `.css` vào **trong cùng một thư mục**, ta có thể dùng lệnh đơn giản `sass <folder>` (bỏ qua output files). Tuy nhiên, vì thực hiện tự động nên các file `.css` sẽ có cùng tên file với các file `.scss`.
> 
> ```
> sass src/styles
> ```
> 
> - Cũng như trường hợp trên, nhưng không muốn các file `.css` được biên dịch vào cùng một thư mục với các file `.scss`, ta có thể dùng lệnh `sass <input-folder>:<output-folder>`.
>
> ```
> sass src/scss:src/css 
> ```

Lệnh `sass` đơn thuần chỉ biên dịch (các) file `.scss` 1 lần duy nhất. Để có thể theo dõi các thay đổi và biên dịch lại tự động trong quá trình phát triển, hãy thêm flag `--watch`. Các thay đổi trên file `.scss` sẽ được đồng bộ biên dịch vào các file `.css` tương ứng.

**Ví dụ:**

```
sass --watch source.scss des.css
```

> [!Note]
>
> Khi sử dụng SASS với các Frontend framework hay library như React.js, Vue.js và Angular, việc biên dịch SASS thường là không cần thiết. Hãy xem tài liệu của từng framework hay library để biết cách sử dụng SASS.

## Sử dụng SASS

### # Biến - Variables

Khác với biến trong CSS bằng cách khai báo với tiền tố `--` và phải sử dụng `var()`, biến trong SASS chỉ cần sử dụng ký hiệu `$`.

**Ví dụ:**

- SCSS:

```scss
$text-color: #333;
$size: 16px;

h1 {
  font-size: $size;
  color: $text-color;
}
```

- CSS:

```css
h1 {
  font-size: 16px;
  color: #333;
}
```

Biến trong SCSS có thể khai báo toàn cục bên ngoài hoặc cục bộ bên trong style.

> [!Note]
>
> Biến trong SCSS không biên dịch thành các biến CSS mà sẽ được biên dịch trực tiếp giá trị vào các vị trí sử dụng biến.

### Cú pháp lồng - Nesting

CSS không có cú pháp lồng nhau và thể hiện quan hệ giữa các selector như HTML. Với SCSS, ta có thể thể hiện điều đó.

**Ví dụ:**

- SCSS:

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

- CSS:

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li { display: inline-block; }

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

#### ## Selector list

Ta có thể dùng dấu phẩy để phân cách các selector có cùng style và có cùng cấu trúc nếu có sử dụng cú pháp lồng.

**Ví dụ:**

- SCSS:

```scss
.message, .notification {
  display: flex;
  align-items: center;

  .content {
    font-size: 18px;
  }

  .link {
    color: #357afa;
    text-decoration: none;
  }
}
```

- CSS:

```css
.message, .notification {
  display: flex;
  align-items: center;
}

.message .content, .notification .content {
  font-size: 18px;
}

.message .link, .notification .link {
  color: #357afa;
  text-decoration: none;
}
```

#### ## Selector Combinators

Theo mặc định, cú pháp lồng dùng Descendant selector (`parent child`) để thể hiện quan hệ giữa 2 selector.

**Ví dụ:**

- SCSS:

```scss
ul {
  list-style: none;

  li {
    padding: 10px;
  }
}
```

- CSS:

```css
ul {
  list-style: none;
}

// Descendant selector
ul li {
  padding: 10px;
}
```

Muốn chỉ định các Compinator khác, hãy đặt các ký hiệu combinator ở cuối selector cha, ở đầu selector con hoặc đặt ở giữa 2 selector. Giữa chúng sẽ có một số điều khác biệt.

- **Đặt ở cuối selector cha**: áp dụng combinator cho các selector con.

**Ví dụ:**

```scss
// SCSS
.message > {
  .content {
    color: red;
  }
  .link {
    color: green;
  }
}

// CSS
.message > .content {
  color: red;
}
.message > .link {
  color: green;
}
```

- **Đặt ở phía trước selector con**: chỉ selector con mới sử dụng combinator chỉ định.

**Ví dụ:**

```scss
// SCSS
.message {
  + .content {
    color: red;
  }
  .link {
    color: green;
  }
}

// CSS
.message + .content {
  color: red;
}
.message .link {
  color: green;
}
```

- **Đặt ở giữa 2 selector**: cú pháp này cho phép nhóm các kiểu combinator.

```scss
// SCSS
.message {
  // các selector con sử dụng combinator `~`
  ~ { 
    .content {
      color: red;
    }
    .link {
      color: green;
    }
  }
  // các selector con sử dụng combinator `+`
  + {
    .other {
      color: blue;
    }
  }
}

// CSS
.message ~ .content {
  color: red;
}
.message ~ .link {
  color: green;
}
.message + .other {
  color: blue;
}
```

### # Ký hiệu `&` - Parent selector

Trong cú pháp lồng, ta có thể sử dụng ký hiệu `&` để tái sử dụng tên selector cha.

**Ví dụ:**

- HTML:

```html
<div class='message'>
  <p class='message-content'>Lorem ipsum dolor sit amet</p>
  <a class='message-link' href='my-link'>Click me</a>
</div>
```

- SCSS:

```scss
.message {
  border: 1px solid #777;
  &-content {
    color: #333;
    font-size: 14px;
  }
  &-link {
    text-decoration: none;
    color: lightblue;
  }
}
```

- CSS:

```css
.message {
  border: 1px solid #777;
}

.message-content {
  color: #333;
  font-size: 14px;
}

.message-link {
  text-decoration: none;
  color: lightblue;
}
```

Ký hiệu `&` cũng có thể sử dụng với các Pseudo class hoặc Pseudo element như `:hover`, `:first-child`, `::before`, ...

**Ví dụ:**

```scss
.content {
  position: relative;

  &:hover {
    font-weight: 600;
    font-style: italic;
  }

  &::after {
    position: absolute;
    content: '';
    // scss ...
  }
}
```

### # `@mixin` và `@include`

Mixin có thể hiểu là một loại cú pháp hàm trong SCSS. Nó cho phép tái sử dụng các style và cũng như có thể nhận tham số để linh hoạt trong việc tạo kiểu.

Cú pháp:

```
@mixin <mixin-name>(<params>) {
  // scss ...
}
```

Trong đó:

- **`<mixin-name>`** không bắt đầu bằng ký hiệu `$`.

- **`<params>`** là các tham số cho mixin. Các tham số này có thể hiểu là biến cho mixin, cú pháp tương tự biến. Thành phần này có thể không có khi tạo mixin.

**Ví dụ:**

```scss
@mixin flexCenter() {
  display: flex;
  align-items: center;
}

@mixin fontStyle($style, $color) {
  font-style: $style;
  color: $color;
}
```

Để sử dụng mixin, ta sử dụng `@include` theo sau là tên của mixin và các giá trị cho tham số.

```scss
@include <mixin-name>(<arguments>)
```

**Ví dụ:**

```scss
.content {
  @include flexCenter();
  // hoặc
  @include flexCenter; // trường hợp mixin không nhận tham số nào
}

.message {
  @include fontStyle(italic, #333)
}
```

> [!Tip]
>
> Các tham số của mixin có thể nhận giá trị mặc định. Để chỉ định giá trị mặc định, ta sẽ sử dụng cú pháp: `param: defaultValue`.

Bên trong mixin có thể sử dụng `@include` để sử dụng một mixin khác.

**Ví dụ**:

```scss
@mixin reset-list {
  margin: 0;
  padding: 0;
  list-style: none;
}

@mixin horizontal-list {
  @include reset-list;

  li {
    display: inline-block;
    margin: {
      left: -2px;
      right: 2em;
    }
  }
}

nav ul {
  @include horizontal-list;
}
```

### # `@extend`

Trong SCSS, để có thể tái sử dụng lại style từ một selector khác, không chỉ sử dụng mixin mà ta cũng có thể sử dụng từ khoá `@extend` để thực hiện kế thừa lại style của một selector khác.

**Ví dụ:**

- SCSS:

```scss
.message {
  color: green;
  font-size: 12px;
}

.content {
  @extend .message;
  font-weight: 600;
}
```

- CSS:

```css
.message, .content {
  color: green;
  font-size: 12px;
}

.content {
  font-weight: 600;
}
```

Nếu muốn tạo một style chỉ có mục đích cho kế thừa (không sử dụng riêng lẻ), thì ta có thể đặt tên cho style và bắt đầu bằng `%`.

**Ví dụ:**

- SCSS:

```scss
%link {
  text-decoration: none;
  color: #3676ff;
  cursor: pointer;
}

.button-link {
  @extend %link;
  border: 1px solid #777;
  outline: none;
  border-radius: 10px;
}

.text-link {
  @extend %link;
  cursor: text;
}
```

- CSS:

```css
.text-link, .button-link {
  text-decoration: none;
  color: #3676ff;
  cursor: pointer;
}

.button-link {
  border: 1px solid #777;
  outline: none;
  border-radius: 10px;
}

.text-link {
  cursor: text;
}
```

> [!Warning]
>
> SCSS chỉ cho phép kế thừa trên một selector đơn giản và độc lập, ví dụ như `.tab.active` được xem là một selector phức tạp.


