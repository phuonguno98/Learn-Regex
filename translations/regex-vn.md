<a href="https://www.facebook.com/phuonguno.vn" target="_blank"><img src="../img/facebook-link.PNG" alt="Nguyen Thanh Phuong" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

<p align="center">
    <br/>
    <a href="https://github.com/phuonguno98/learn-regex">
        <img src="/img/learn-regex.PNG" alt="Learn Regex">
    </a>
    <br /><br />
    <p>
        <a href="https://www.github.com/phuonguno98">
            <img src="https://img.shields.io/github/followers/phuonguno98?style=social" />
        </a>
    </p>
</p>



## Biểu thức chính quy là gì?

> Biểu thức chính quy là một nhóm các ký tự hoặc ký hiệu được sử dụng để tìm một mẫu cụ thể từ một văn bản.

Biểu thức chính quy là một khuôn mẫu được khớp với chuỗi các từ, từ trái sang phải. Từ "Biểu thức chính quy" là một câu cửa miệng, bạn thường sẽ tìm thấy thuật ngữ viết tắt là "regex" hoặc "regexp". Biểu thức chính quy được sử dụng để thay thế một văn bản trong một chuỗi, xác thực mẫu, trích xuất một chuỗi con từ một chuỗi dựa trên khớp mẫu và hơn thế nữa.

Hãy tưởng tượng bạn đang viết một ứng dụng và bạn muốn đặt quy tắc khi người dùng chọn tên người dùng của họ. Chúng tôi muốn cho phép tên người dùng chứa các chữ cái, số, dấu gạch dưới và dấu gạch nối. Chúng tôi cũng muốn giới hạn số lượng ký tự trong tên người dùng để nó trông không xấu. Chúng tôi sử dụng biểu thức chính quy sau để xác thực tên người dùng:



<br/><br/>
<p align="center">
  <img src="../img/regexp-en.png" alt="Regular expression">
</p>



Biểu thức chính quy trên có thể chấp nhận các chuỗi `john_doe`, `jo-hn_doe` và `john12_as`. Nó không khớp với `Jo` vì chuỗi đó chứa chữ hoa và nó quá ngắn.

## Table of Contents

- [Basic Matchers](#1-basic-matchers)
- [Meta character](#2-meta-characters)
  - [Full stop](#21-full-stop)
  - [Character set](#22-character-set)
    - [Negated character set](#221-negated-character-set)
  - [Repetitions](#23-repetitions)
    - [The Star](#231-the-star)
    - [The Plus](#232-the-plus)
    - [The Question Mark](#233-the-question-mark)
  - [Braces](#24-braces)
  - [Character Group](#25-character-group)
  - [Alternation](#26-alternation)
  - [Escaping special character](#27-escaping-special-character)
  - [Anchors](#28-anchors)
    - [Caret](#281-caret)
    - [Dollar](#282-dollar)
- [Shorthand Character Sets](#3-shorthand-character-sets)
- [Lookaround](#4-lookaround)
  - [Positive Lookahead](#41-positive-lookahead)
  - [Negative Lookahead](#42-negative-lookahead)
  - [Positive Lookbehind](#43-positive-lookbehind)
  - [Negative Lookbehind](#44-negative-lookbehind)
- [Flags](#5-flags)
  - [Case Insensitive](#51-case-insensitive)
  - [Global search](#52-global-search)
  - [Multiline](#53-multiline)
- [Greedy vs lazy matching](#6-greedy-vs-lazy-matching)


## 1. Basic Matchers


Biểu thức chính quy là một mẫu các ký tự mà chúng ta sử dụng để thực hiện tìm kiếm trong văn bản. Ví dụ, biểu thức chính quy `the` có nghĩa là: chữ `t`, tiếp theo là chữ `h`, tiếp theo là chữ `e`.

<pre>
"the" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Test the regular expression](https://regex101.com/r/dmRygT/1)

Biểu thức chính quy `123` khớp với chuỗi `123`. Biểu thức chính quy được khớp với chuỗi đầu vào bằng cách so sánh từng ký tự trong biểu thức chính quy với từng ký tự trong chuỗi đầu vào, lần lượt từng ký tự. Biểu thức chính quy thường phân biệt chữ hoa chữ thường nên biểu thức chính quy `The` sẽ không khớp với chuỗi `the`.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/1paXsy/1)

## 2. Meta Characters

Các ký tự `meta` là các khối xây dựng của các biểu thức chính quy. Các ký tự `meta` không biểu diễn chính nó mà thay vào đó được diễn giải theo một cách đặc biệt nào đó. Một số ký tự `meta` có ý nghĩa đặc biệt và được viết bên trong dấu ngoặc vuông. Các ký tự meta như sau:

|Meta character|Description|
|:----:|----|
|.|Khớp với tất cả các kí tự trừ dấu xuống dòng.|
|[ ]|Lớp kí tự. Khớp với bất kỳ ký tự nào chứa trong dấu ngoặc vuông.|
|[^ ]|Lớp kí tự phủ định. Khớp với bất kỳ ký tự nào không có trong dấu ngoặc vuông.|
|*|Khớp 0 hoặc nhiều lần lặp lại của kí tự trước.|
|+|Khớp 1 hoặc nhiều lần lặp lại của kí tự trước.|
|?|Làm cho kí tự trước tùy chọn.|
|{n,m}|Braces. Khớp ít nhất là "n" lần nhưng không nhiều hơn "m" lần lặp lại của kí tự trước.|
|(xyz)|Nhóm kí tự. Khớp các ký tự xyz theo thứ tự chính xác đó.|
|&#124;|Thay thế. Khớp các ký tự trước hoặc ký tự sau ký hiệu.|
|&#92;|Thoát khỏi kí tự tiếp theo. Điều này cho phép bạn khớp các ký tự dành riêng <code>[ ] ( ) { } . * + ? ^ $ \ &#124;</code>|
|^|Khớp ở đầu của đầu vào.|
|$|Khớp ở cuối của đầu vào.|

## 2.1 Full stop


Full stop `.`  là ví dụ đơn giản nhất về ký tự meta. Kí tự meta `.`
khớp với bất kì kí tự nào. Nó sẽ không khớp kí tự trả về (return) hoặc xuống dòng (newline)

Ví dụ, biểu thức chính quy `.ar` có ý nghĩa: bất kỳ ký tự nào, theo sau là chữ `a`, tiếp theo là chữ `r`.

<pre>
".ar" => The <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/xc9GkU/1)

## 2.2 Character set

Bộ ký tự cũng được gọi là lớp kí tự. Dấu ngoặc vuông được sử dụng để chỉ định bộ ký tự. Sử dụng dấu gạch nối bên trong bộ ký tự để chỉ định phạm vi của các ký tự. Thứ tự của phạm vi ký tự trong dấu ngoặc vuông không quan trọng. 

Ví dụ: biểu thức chính quy `[Tt]he` có nghĩa là: chữ hoa `T` hoặc chữ thường `t`, theo sau là chữ `h`, tiếp theo là chữ `e`.

<pre>
"[Tt]he" => <a href="#learn-regex"><strong>The</strong></a> car parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/2ITLQ4/1)


Tuy nhiên, dấu chấm `.` gian bên trong một bộ ký tự có nghĩa là một dấu chấm `.` theo nghĩa đen. Biểu thức chính quy `ar[.]` Có nghĩa là: ký tự chữ thường `a`, theo sau là chữ `r`, theo sau là kí tự `.` .

<pre>
"ar[.]" => A garage is a good place to park a c<a href="#learn-regex"><strong>ar.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/wL3xtE/1)

### 2.2.1 Negated character set

Nói chung, biểu tượng dấu mũ biểu thị sự bắt đầu của chuỗi, nhưng khi nó được gõ sau dấu ngoặc vuông mở, nó sẽ phủ định bộ ký tự. Ví dụ: biểu thức chính quy `[^ c]ar` có nghĩa là: bất kỳ ký tự nào ngoại trừ `c`, theo sau là ký tự `a`, theo sau là chữ `r`.

<pre>
"[^c]ar" => The car <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/nNNlq3/1)




## 2.3 Repetitions

Các ký tự meta, `+`, `*` hoặc `?` được sử dụng để xác định số lần một `pattern` có thể xuất hiện. Những kí tự meta này hoạt động khác nhau trong các tình huống khác nhau.


### 2.3.1 The Star

Ký tự `*` khớp 0 hoặc nhiều lần lặp lại của trình so khớp trước. Biểu thức chính quy `a*` có nghĩa là: 0 hoặc nhiều lần lặp lại ký tự chữ thường `a`. Nhưng nếu nó xuất hiện sau một bộ ký tự hoặc lớp thì nó sẽ tìm thấy sự lặp lại của toàn bộ bộ ký tự. Ví dụ: biểu thức chính quy `[a-z]*` có nghĩa là: bất kỳ số lượng chữ cái viết thường trong một hàng.

<pre>
"[a-z]*" => T<a href="#learn-regex"><strong>he</strong></a> <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>parked</strong></a> <a href="#learn-regex"><strong>in</strong></a> <a href="#learn-regex"><strong>the</strong></a> <a href="#learn-regex"><strong>garage</strong></a> #21.
</pre>

[Test the regular expression](https://regex101.com/r/7m8me5/1)

Ký tự `*` có thể được sử dụng với ký tự meta `.` để khớp với bất kỳ chuỗi ký tự nào `.*` . Ký tự `*` có thể được sử dụng với ký tự khoảng trắng `\s` để khớp với một chuỗi các ký tự khoảng trắng. 

Ví dụ: biểu thức `\s*cat\s*` có nghĩa là: không hoặc nhiều khoảng trắng, theo sau là ký tự chữ thường `c`, theo sau là ký tự chữ thường `a`, theo sau là ký tự chữ thường `t`, tiếp theo là 0 hoặc nhiều khoảng trắng.


<pre>
"\s*cat\s*" => The fat<a href="#learn-regex"><strong> cat </strong></a>sat on the con<a href="#learn-regex"><strong>cat</strong></a>enation.
</pre>

[Test the regular expression](https://regex101.com/r/gGrwuz/1)




### 2.3.2 The Plus


Ký tự `+` khớp với một hoặc nhiều lần lặp lại của ký tự trước đó. 

Ví dụ: biểu thức chính quy `c.+t` có nghĩa là: chữ thường chữ `c`, theo sau là ít nhất một ký tự, tiếp theo là ký tự chữ thường `t`. Nó thể hiện rõ rằng `t` là `t` cuối cùng trong câu.


<pre>
"c.+t" => The fat <a href="#learn-regex"><strong>cat sat on the mat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/Dzf9Aa/1)

### 2.3.3 The Question Mark

Trong biểu thức chính quy các ký tự meta `?` làm cho ký tự trước là một tùy chọn. Ký tự này khớp với 0 hoặc một thể hiện (instance) của ký tự trước đó. Ví dụ: biểu thức chính quy `[T]?he` có nghĩa là: Tùy chọn chữ hoa chữ `T`, theo sau là ký tự chữ thường `h`, tiếp theo là ký tự chữ thường `e`.

<pre>
"[T]he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[Test the regular expression](https://regex101.com/r/cIg9zm/1)

<pre>
"[T]?he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in t<a href="#learn-regex"><strong>he</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/kPpO2x/1)


## 2.4 Braces


Trong các biểu thức chính quy, các dấu ngoặc nhọn, còn được gọi là bộ định lượng, được sử dụng để chỉ định số lần mà một ký tự hoặc một nhóm ký tự có thể được lặp lại. Ví dụ: biểu thức chính quy `[0-9]{2,3}` có nghĩa là: Khớp ít nhất 2 chữ số nhưng không quá 3 các ký tự trong phạm vi từ 0 đến 9.


<pre>
"[0-9]{2,3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Test the regular expression](https://regex101.com/r/juM86s/1)


Chúng ta có thể bỏ qua đối số thứ hai. Ví dụ: biểu thức chính quy `[0-9]{2,}` có nghĩa là: Khớp ít nhất từ 2 chữ số trở lên. Nếu chúng ta xóa dấu phẩy, biểu thức chính quy `[0-9]{3}` có nghĩa là: khớp chính xác 3 chữ số.

<pre>
"[0-9]{2,}" => The number was 9.<a href="#learn-regex"><strong>9997</strong></a> but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Test the regular expression](https://regex101.com/r/Gdy4w5/1)

<pre>
"[0-9]{3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to 10.0.
</pre>

[Test the regular expression](https://regex101.com/r/Sivu30/1)


## 2.5 Capturing Group

Một nhóm capturing là một nhóm các mẫu con được viết bên trong Dấu ngoặc đơn `(...)`. Giống như chúng ta đã thảo luận trước đó trong biểu thức chính quy nếu chúng ta đặt một bộ định lượng sau một ký tự thì nó sẽ lặp lại ký tự trước. Nhưng nếu chúng ta đặt bộ định lượng sau một nhóm capturing thì nó lặp lại toàn bộ nhóm capturing. Ví dụ: biểu thức chính quy `(ab)*` khớp với 0 hoặc nhiều lần lặp lại của ký tự "ab". Chúng ta cũng có thể sử dụng ký tự meta `|` trong nhóm capturing. Ví dụ: biểu thức chính quy `(c|g|p)ar` có nghĩa là: ký tự chữ thường `c`, `g` hoặc `p`, theo sau là ký tự `a`, tiếp theo là ký tự `r`.



<pre>
"(c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/tUxrBG/1)


Lưu ý rằng các nhóm capturing không chỉ khớp mà còn capture các ký tự để sử dụng trong ngôn ngữ gốc. Ngôn ngữ gốc có thể là python hoặc javascript hoặc hầu như bất kỳ ngôn ngữ nào thực hiện các biểu thức chính quy trong định nghĩa hàm.


### 2.5.1 Non-capturing group

Nhóm Non-capturing là nhóm capturing chỉ khớp các ký tự, nhưng không capture nhóm. Một nhóm Non-capturing được ký hiệu là `?` theo sau là `:` trong ngoặc đơn `(...)`. 

Ví dụ: biểu thức chính quy `(?:c|g|p)ar` tương tự như `(c|g|p)ar` nhưng sẽ không tạo ra một nhóm capture.

<pre>
"(?:c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Test the regular expression](https://regex101.com/r/Rm7Me8/1)

Các nhóm Non-capturing có thể có ích khi được sử dụng trong chức năng tìm và thay thế hoặc khi kết hợp với các nhóm capturing để giữ tổng quan khi sinh ra bất kỳ loại đầu ra nào khác. Xem thêm [4. Lookaround](#4-lookaround). 


## 2.6 Alternation

Trong một biểu thức chính quy, thanh dọc `|` được sử dụng để xác định sự thay thế. Sự thay thế này giống như một câu lệnh OR giữa nhiều biểu thức. Bây giờ, bạn có thể nghĩ rằng bộ ký tự và sự thay thế hoạt động theo cùng một cách. Nhưng sự khác biệt lớn giữa bộ ký tự và sự thay thế là bộ ký tự hoạt động ở cấp độ ký tự, còn sự thay thế sẽ hoạt động ở cấp độ biểu thức.

Ví dụ: biểu thức chính quy `(T|t)he|car` có nghĩa là: hoặc (ký tự chữ `T` hoặc chữ thường `t`, theo sau là ký tự chữ thường `h`, tiếp theo là ký tự chữ thường `e`) HOẶC (ký tự chữ thường `c`, tiếp theo là ký tự chữ thường `a`, theo sau bằng ký tự viết thường `r`). Lưu ý rằng tôi đặt dấu ngoặc đơn cho rõ ràng, để cho thấy rằng một trong hai biểu thức trong ngoặc đơn có thể được đáp ứng và nó sẽ khớp.

<pre>
"(T|t)he|car" => <a href="#learn-regex"><strong>The</strong></a> <a href="#learn-regex"><strong>car</strong></a> is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/fBXyX0/1)

## 2.7 Escaping special character


Dấu gạch chéo ngược `\` được sử dụng trong biểu thức chính quy để thoát ký tự tiếp theo. Điều này cho phép chúng ta chỉ định các ký tự dành riêng `{} [] / \ *. $ ^ | ?` là một ký tự so khớp bình thường. Để sử dụng một trong số các ký tự đặc biệt này, ta dùng `\` làm ký tự so khớp trước kí tự ta muốn dùng.

Ví dụ, biểu thức chính quy `.` được sử dụng để khớp với bất kỳ ký tự nào ngoại trừ dòng mới. Bây giờ, để khớp dấu chấm `.` trong một chuỗi đầu vào, ví dụ, biểu thức chính quy `(f|c|m)at\.?` có nghĩa là: chữ thường `f`, `c` hoặc `m`, theo sau là ký tự chữ thường `a`, tiếp theo là chữ thường chữ `t`, theo sau là ký tự tùy chọn `.`.


<pre>
"(f|c|m)at\.?" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> sat on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/DOc5Nu/1)


## 2.8 Anchors


Trong các biểu thức chính quy, chúng ta sử dụng các anchors để kiểm tra xem ký tự so khớp là ký tự bắt đầu hay ký tự kết thúc của chuỗi đầu vào. Các anchors có hai loại: Loại thứ nhất là Caret `^` kiểm tra xem ký tự khớp có phải là ký tự bắt đầu của đầu vào không và loại thứ hai là Dollar `$` kiểm tra xem ký tự khớp có phải là ký tự cuối cùng của chuỗi đầu vào không.




### 2.8.1 Caret


Biểu tượng Caret `^` được sử dụng để kiểm tra xem ký tự khớp có phải là ký tự đầu tiên của chuỗi đầu vào không. Nếu chúng ta áp dụng biểu thức chính quy sau `^a` (nghĩa là a phải là ký tự bắt đầu) cho chuỗi đầu vào `abc` thì nó sẽ khớp `a`. Nhưng nếu chúng ta áp dụng biểu thức chính quy `^b` trên chuỗi đầu vào ở trên thì nó không khớp với bất cứ thứ gì. Bởi vì trong chuỗi đầu vào `abc` "b" không phải là ký tự bắt đầu. Chúng ta hãy xem một biểu thức chính quy khác `^(T|t)he` có nghĩa là: ký tự chữ hoa `T` hoặc ký tự chữ thường `t` phải là ký tụ bắt đầu của chuỗi đầu vào, tiếp theo là ký tự chữ thường `h`, tiếp theo là ký tự chữ thường `e`.


<pre>
"(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Test the regular expression](https://regex101.com/r/5ljjgB/1)

<pre>
"^(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[Test the regular expression](https://regex101.com/r/jXrKne/1)

### 2.8.2 Dollar


Ký tự Dollar `$` được sử dụng để kiểm tra xem ký tự khớp có phải là ký tự cuối cùng của chuỗi đầu vào không. Ví dụ: biểu thức chính quy `(at\.)$` có nghĩa là: ký tự chữ thường `a`, theo sau là ký tự chữ thường `t`, theo sau là ký tự `.` và bộ so khớp phải là cuối chuỗi.



<pre>
"(at\.)" => The fat c<a href="#learn-regex"><strong>at.</strong></a> s<a href="#learn-regex"><strong>at.</strong></a> on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/y4Au4D/1)

<pre>
"(at\.)$" => The fat cat. sat. on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/t0AkOd/1)

##  3. Shorthand Character Sets



Biểu thức chính quy cung cấp các shorthand cho các bộ ký tự thường được sử dụng. Các bộ ký tự shorthand như sau:


|Shorthand|Description|
|:----:|----|
|.| Bất kỳ kí tự nào ngoại trừ dòng mới|
|\w|Khớp các ký tự chữ và số: `[a-zA-Z0-9_]`|
|\W|Khớp các ký tự không phải chữ và số: `[^\w]`|
|\d|khớp với số trong khoảng: `[0-9]`|
|\D|Khớp không có chữ số: `[^\d]`|
|\s|Khớp các ký tự khoảng trắng: `[\t\n\f\r\p{Z}]`|
|\S|Khớp với ký tự không phải khoảng trắng: `[^\s]`|

## 4. Lookaround

Lookbehind và lookahead (còn được gọi là lookaround) là các loại nhóm ***Non-capturing*** (được sử dụng để khớp với mẫu nhưng không được bao gồm trong danh sách phù hợp). `Lookarounds` sử dụng khi chúng ta có điều kiện mẫu đi trước hoặc theo sau bởi một mẫu khác. 

Ví dụ: chúng ta muốn nhận tất cả các số có trước ký tự `$` từ chuỗi đầu vào sau `$4,44 và $10,88`. Chúng tôi sẽ sử dụng biểu thức chính quy sau `(?<=\$)[0-9\.]*` có nghĩa là: lấy tất cả các số có chứa ký tự `.` và đứng trước là ký tự `$`. Sau đây là những lookaround được sử dụng trong các biểu thức thông thường:

|Kí hiệu|Mô tả|
|:----:|----|
|?=|Positive Lookahead|
|?!|Negative Lookahead|
|?<=|Positive Lookbehind|
|?<!|Negative Lookbehind|

### 4.1 Positive Lookahead


`Positive lookahead` xác định phần đầu tiên của biểu thức phải được theo sau bởi một biểu thức cụ thể nào đó. Phần khớp trả về (The returned match) chỉ chứa văn bản được khớp bởi phần đầu tiên của biểu thức. Để xác định một `positive lookahead`, ta sử dụng dấu ngoặc đơn. Trong dấu ngoặc đơn đó, có một dấu hỏi và dấu bằng kề nhau được sử dụng như thế này: `(?=...)`. Biểu thức `Lookahead` được viết sau dấu bằng trong ngoặc đơn. 

Ví dụ: biểu thức chính quy `(T|t)he(?=\sfat)` có nghĩa là: khớp chữ thường `t` hoặc chữ hoa `T`, theo sau là chữ `h`, tiếp theo là chữ `e`. Trong ngoặc đơn, chúng ta xác định một `positive lookahead` cho biết công cụ (engine) biểu thức chính quy khớp với `The` hoặc `the` mà có ký tự trắng `\s` và từ `fat` theo sau nó.


<pre>
"(T|t)he(?=\sfat)" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/IDDARt/1)

### 4.2 Negative Lookahead


`Negative lookahead` được sử dụng khi chúng ta cần lấy tất cả các kết quả khớp từ chuỗi đầu vào mà nó không được theo sau bởi một mẫu cụ thể nào đó. `Negative lookahead` được định nghĩa giống như chúng ta định nghĩa `positive lookahead` nhưng sự khác biệt duy nhất là thay vì bằng ký tự `=` chúng ta sử dụng kí tự phủ định `!`  tức là `(?! ...)`. 

Chúng ta hãy xem biểu thức chính quy sau đây: `(T|t)he(?!\sfat)` có nghĩa là: lấy tất cả các từ `The` hoặc `the` từ chuỗi đầu vào mà không có ký tự trắng `\s` và từ `fat` theo sau nó.

<pre>
"(T|t)he(?!\sfat)" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Test the regular expression](https://regex101.com/r/V32Npg/1)

### 4.3 Positive Lookbehind

`Positive lookbehind` được sử dụng để lấy tất cả mẫu khớp nếu trước nó có một mẫu nào đó  cụ thể. `Positive lookbehind` được biểu thị bởi `(?<=...)`. 

Ví dụ: biểu thức chính quy `(?<=(T|t)he\s)(fat|mat)` có nghĩa là: lấy tất cả các từ `fat` hoặc `mat` từ chuỗi đầu vào nếu có từ `The` hoặc `the` và ký tự trắng `\s` đứng trước nó.



<pre>
"(?<=(T|t)he\s)(fat|mat)" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/avH165/1)

### 4.4 Negative Lookbehind


`Negative lookbehind` được sử dụng để lấy tất cả các mẫu khớp nếu trước nó không có một mẫu nào đó cụ thể. `Negative lookbehind` được ký hiệu là `(?<!...)`. 

Ví dụ: biểu thức chính quy `(?<!(T|t)he\s)(cat)` có nghĩa là: lấy tất cả các từ `cat` từ chuỗi đầu vào nếu không có từ `The` hoặc `the` và ký tự trắng `\s` đứng trước.

<pre>
"(?&lt;!(T|t)he\s)(cat)" => The cat sat on <a href="#learn-regex"><strong>cat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/8Efx5G/1)

## 5. Flags


Cờ (flags) cũng được gọi là bổ nghĩa (modifiers) vì chúng sửa đổi đầu ra của biểu thức chính quy. Các cờ này có thể được sử dụng theo bất kỳ thứ tự hoặc kết hợp nào và là một phần không thể thiếu của RegExp.



|Cờ|Mô tả|
|:------:|----|
|i|Case insensitive: Khớp với mẫu không phân biệt chữ hoa chữ thường.|
|g|Global Search: Tìm kiếm tất cả mẫu trong toàn bộ đầu vào.|
|m|Multiline: ký tự Anchor meta hoạt động trên từng dòng (có nhiều dòng).|

### 5.1 Case Insensitive


Cờ `i` được sử dụng để thực hiện khớp mẫu không phân biệt chữ hoa chữ thường. 

Ví dụ: biểu thức chính quy `/The/gi` có nghĩa là: chữ hoa `T`, theo sau là ký tự chữ thường `h`, tiếp theo là ký tự `e`. Và ở cuối biểu thức chính quy, cờ `i` báo cho công cụ biểu thức chính quy khớp không phân biệt chữ hoa chữ thường. Như bạn có thể thấy, chúng tôi cũng đã cung cấp cờ `g` vì chúng tôi muốn tìm kiếm mẫu trong toàn bộ chuỗi đầu vào.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/dpQyf9/1)

<pre>
"/The/gi" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Test the regular expression](https://regex101.com/r/ahfiuh/1)

### 5.2 Global search


Cờ `g` được sử dụng để thực hiện khớp tất cả các mẫu phù hợp trên toàn bộ đầu vào (tìm tất cả các từ có thể khớp thay vì dừng sau lần khớp đầu tiên). 

Ví dụ: biểu thức chính quy `/.(at)/g` có nghĩa là: bất kỳ ký tự nào ngoại trừ dòng mới, theo sau là ký tự chữ thường `a`, tiếp theo là ký tự chữ thường `t`. Vì chúng tôi đã cung cấp cờ `g` ở cuối biểu thức chính quy nên bây giờ nó sẽ tìm thấy tất cả các kết quả khớp trong chuỗi đầu vào, không chỉ là lần khớp đầu tiên (là hành động mặc định).

<pre>
"/.(at)/" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the mat.
</pre>

[Test the regular expression](https://regex101.com/r/jnk6gM/1)

<pre>
"/.(at)/g" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> <a href="#learn-regex"><strong>sat</strong></a> on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[Test the regular expression](https://regex101.com/r/dO1nef/1)

### 5.3 Multiline


Cờ `m` được sử dụng để thực hiện khớp trên nhiều dòng. Như chúng ta đã thảo luận về các anchors `(^, $)` trước đó, được sử dụng để kiểm tra xem mẫu là phần đầu của chuỗi đầu vào hay phần cuối của chuỗi đầu vào. Nhưng nếu chúng ta muốn các anchors hoạt động trên mỗi dòng, chúng ta sử dụng cờ `m`. 

Ví dụ: biểu thức chính quy `/at(.)?$/gm` có nghĩa là: ký tự chữ thường `a`, theo sau là ký tự chữ thường `t`, tùy chọn mọi thứ trừ dòng mới. Và vì cờ `m` bây giờ công cụ biểu thức chính quy khớp với mẫu ở cuối mỗi dòng trong một chuỗi đầu vào.


<pre>
"/.at(.)?$/" => The fat
                cat sat
                on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/hoGMkP/1)

<pre>
"/.at(.)?$/gm" => The <a href="#learn-regex"><strong>fat</strong></a>
                  cat <a href="#learn-regex"><strong>sat</strong></a>
                  on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Test the regular expression](https://regex101.com/r/E88WE2/1)




## 6. Greedy vs lazy matching


Theo mặc định, regex sẽ thực hiện greedy matching, có nghĩa là nó sẽ khớp tất cả các mẫu phù hợp trong toàn bộ đầu vào. Chúng ta có thể sử dụng `?` để thực hiện chỉ khớp với một  mẫu phù hợp đầu tiên tìm thấy.




<pre>
"/(.*at)/" => <a href="#learn-regex"><strong>The fat cat sat on the mat</strong></a>. </pre>


[Test the regular expression](https://regex101.com/r/AyAdgJ/1)

<pre>
"/(.*?at)/" => <a href="#learn-regex"><strong>The fat</strong></a> cat sat on the mat. </pre>


[Test the regular expression](https://regex101.com/r/AyAdgJ/2)


## [Back to main page](../README.md)
