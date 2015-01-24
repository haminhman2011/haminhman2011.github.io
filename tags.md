---
layout: page
title: Rails
comments: yes
premalink: /tags/
---
### Đây là ý nghie4 về một số khái niệm và ý nghĩ các từ khóa cơ bản trong Rails

## I. ActiveRecord là gì?
ActiveRecord thực hiện query trên database. Nó tương thích với hầu hết database systems thông thường như MySQL, SQLite, PostgreSQL.
Format của ActiveRecord method là như nhau với mọi database systems nên việc sử dụng là rất dễ dàng.
ActiveRecord tự động map Ruby object tới table tương ứng trong database.
2 thành phần quan trọng của ActiveRecord là ActiveRecord::Base và ActiveRecord::Validations

Class ActiveRecord::Base là base class của mọi class được ActiveRecord map tới database.
{% highlight Bash shell scripts linenos%}
class User < ActiveRecord::Base
{% endhighlight %}
