---
layout: page
title: Ruby
permalink: /categories/
---

## Số và Phép toán trong Ruby
### Các hàm chuyển số trong Ruby:
{% highlight Bash shell scripts linenos%}
to_i: chuyển về số nguyên

to_f: chuyển về số thập phân

round: chuyển theo qui tắc làm tròn.
{% endhighlight %}
### Các phép toán so sánh trong Ruby:
{% highlight Bash shell scripts linenos%}
>: so sánh lớn hơn

<: so sánh bé hơn

>=: so sánh lớn hơn hoặc bằng

<=: so sánh bé hơn hoặc bằng

==: so sánh bằng nhau
!=: so sánh khác nhau
{% endhighlight %}
## Chuỗi trong Ruby (Ruby String)
Chuỗi, ký tự hay văn bản trong Ruby sẽ được viết trong dấu “noi dung” hoặc là ‘noidung’ tuỳ theo trường hợp sẽ sử dụng. Nếu như trong chuỗi có xuất hiện dấu ngoặc 1 nháy thì ta sử dụng ngoặc kép và ngược lại nếu trong chuỗi có dấu ngoặc kép thì ta sử dụng dấu ngoặc 1 nháy.

Khởi tạo biến và gán chuỗi vào biến:
{% highlight Bash shell scripts linenos%}
a = "hello"
b = "ruby"
{% endhighlight %}
Cộng chuỗi dùng phép toán cộng (+)
{% highlight Bash shell scripts linenos%}
a+b => "helloruby"
a+" "+b => "hello ruby"
{% endhighlight %}
Dùng phép nhân (*) để in ra nhiều lần giá trị của chuỗi
{% highlight Bash shell scripts linenos%}
a * 5 => "hellohellohellohellohello"
"rails" * 5 => "railsrailsrailsrailsrails"
{% endhighlight %}
So sánh chuỗi, kết quả sẽ trả về true nếu đúng và false nếu sai:
So sánh bằng(sử dụng: ==)
{% highlight Bash shell scripts linenos%}
a == "hello" => true
a == "ruby" => false
{% endhighlight %}
So sánh không bằng(sử dụng: !=) hay còn gọi là so sánh khác nhau:
{% highlight Bash shell scripts linenos%}
a != "hello" => true
a != b => false
{% endhighlight %}
Đảo chuỗi bằng hàm reverse
{% highlight Bash shell scripts linenos%}
a.reverse => "olleh"
{% endhighlight %}
Đảo chuỗi và gán giá trị vào biến vừa đảo: sử dụng dấu chấm than (!) phía sau reverse
{% highlight Bash shell scripts linenos%}
a.reverse! => "olleh"
{% endhighlight %}
Đếm chiều dài chuỗi sử dụng hàm length, kết quả trả về là số
{% highlight Bash shell scripts linenos%}
a.length => 5
{% endhighlight %}
Chuyển đổi từ kiểu bất kỳ sang kiểu chuỗi(string) sử dụng to_s:
{% highlight Bash shell scripts linenos%}
c = 100
c.to_s => "100"
c.to_s.length => 3
{% endhighlight %}
Nối chuỗi sử dụng hàm concat()
{% highlight Bash shell scripts linenos%}
a.concat(" ruby") => "hello ruby"
# Giá trị biến a được cập nhật là và lúc này a => "hello ruby"
# Thực hiện nối chuỗi một lần nữa với biến b (b lúc này có giá trị là "ruby")
a.concat(b) => "hello rubyruby"
{% endhighlight %}
Tìm kiếm và thay thế trong Ruby sử dụng hàm gsub(‘tìm cái gì’,'thay thế bằng cái này’)
{% highlight Bash shell scripts linenos%}
# biến a lúc này có giá trị là "hello rubyruby"
# tìm kiếm: "rubyruby" và thay thế bằng "ruby" bằng hàm gsub() ta viết như sau
a.gsub('rubyruby','ruby')
# gán kết quả mới vào biến a ta sử dụng phép gán như sau
a = a.gsub('rubyruby','ruby')
{% endhighlight %}
Cắt chuỗi theo một ký tự(nhiều ký tự liên tục) để xử lý ta dùng hàm split(‘ký tự cần tìm để cắt’), kết quả trả về là một mảng chứa các phần tử. Có thể hiểu cắt ở đây là chia chuỗi ra thành nhiều phần.
{% highlight Bash shell scripts linenos%}
# biến a lúc này có giá trị là "hello ruby"
# cắt(hay chia) biến a dựa vào khoảng trắng " " để lấy các từ(word) ta dùng split và viết như sau
a.split(' ') => ["hello","ruby"]
{% endhighlight %}
Mỗi ký tự trong chuỗi của Ruby tương ứng với một vị trí trong mảng
{% highlight Bash shell scripts linenos%}
# biến a lúc này có giá trị là "hello ruby"
a[0] => "h"
a[1] => "e"
a[2] => "l"
a[3] => "l"
a[4] => "o"
a[5] => " "
# ... còn tiếp, mảng bắt đầu từ 0 và tăng dần theo dãy số tự nhiên
{% endhighlight %}
Đếm số lần xuất hiện của một ký tự nào đó dùng hàm count(“ký tự muốn đếm”)
{% highlight Bash shell scripts linenos%}
# biến a lúc này có giá trị là "hello ruby"
a.count("l") => 2
a.count("r") => 1
a.count("z") => 0
# có thể ghi nhiều ký tự liên tục, Ruby sẽ lấy từng ký tự và đếm, sau đó trả về kết quả là phép tính tổng các giá trị
a.count("ell") => 3
a.count("el") => 3
{% endhighlight %}
Kiểm tra chuỗi rỗng hay không(có ký tự hay không) ta dùng hàm empty?
{% highlight Bash shell scripts linenos%}
# biến a lúc này có giá trị là "hello ruby"
a.empty? => false
# khởi tạo biến y và tạo giá trị rỗng
y=""
y.empty? => true
{% endhighlight %}
Xoá bỏ những ký tự khoảng trắng dư thừa(khoảng trắng dư thừa ở đầu hay cuối chuỗi), các ký tự đặc biệt(\n,\t,\r…) sử dụng hàm strip
{% highlight Bash shell scripts linenos%}
# khởi tạo biến x với giá trị là " hello  " : có khoảng trắng dư ở đầu và cuối
x = " hello  "
# dùng strip để xoá
x.strip => "hello"
# khởi tạo biến x với giá trị kèm theo ký tự đặc biệt như \n\t
x = "\n\thello"
# dùng strip để xoá
x.strip => "hello"
{% endhighlight %}
