# SCSS

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

### Cú pháp lồng

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

### # Ký hiệu `&`

Trong cú pháp lồng, ta có thể sử dụng ký hiệu `&` để tái sử dụng tên selector cha. Ký hiệu `&` luôn phải bắt đầu selector.

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

### Mixin và Extend/Inheritance





