---
layout: page
title: Rails
comments: yes
premalink: /tags/
---
### Đây là ý nghĩa  về một số khái niệm và ý nghĩ các từ khóa cơ bản trong Rails

## I. ActiveRecord là gì?
ActiveRecord thực hiện query trên database. Nó tương thích với hầu hết database systems thông thường như MySQL, SQLite, PostgreSQL.
Format của ActiveRecord method là như nhau với mọi database systems nên việc sử dụng là rất dễ dàng.
ActiveRecord tự động map Ruby object tới table tương ứng trong database.
2 thành phần quan trọng của ActiveRecord là ActiveRecord::Base và ActiveRecord::Validations

Class ActiveRecord::Base là base class của mọi class được ActiveRecord map tới database.
{% highlight Bash shell scripts linenos%}
class User < ActiveRecord::Base
{% endhighlight %}
ActiveRecord::Base có các class methods như find(), first()… và các instance methods như save(), delete(), giúp ta thực hiện các câu query trên database.
{% highlight Bash shell scripts linenos%}
u = User.first
u.name = "John"
u.save
{% endhighlight %}
Module ActiveRecord::Validations có các validation methods như valid?(), validates_length_of()
{% highlight Bash shell scripts linenos%}
class User < ActiveRecord::Base
validates_length_of :name, :maximum => 6
end
{% endhighlight %}

## II. Query trong ActiveRecord

Ta có một database với 2 tables như sau:
{% highlight Bash shell scripts linenos%}
class User < ActiveRecord::Base
attr_accessible :email, :name, :city
has_many :microposts
end


class Micropost < ActiveRecord::Base
attr_accessible :content
belongs_to :user
end
{% endhighlight %}

### 1.find()

Tìm theo primary key:
{% highlight Bash shell scripts linenos%}
User.find(10)
=> SELECT "users".* FROM "users" WHERE "users"."id" = ? LIMIT 1 [["id", 10]]
{% endhighlight %}
Ta có thể truyền vào find() 1 mảng các primary keys. Kết quả trả về là 1 mảng các records tìm được.
{% highlight Bash shell scripts linenos%}
User.find([1, 10])
=> SELECT "users".* FROM "users" WHERE "users"."id" IN (1, 10)
{% endhighlight %}

Tìm theo trường của bảng dữ liệu
{% highlight Bash shell scripts linenos%}
User.find_by_name('John')
=> SELECT "users".* FROM "users" WHERE "users"."name" = 'John' LIMIT 1
{% endhighlight %}
Tìm kiếm theo batches:
{% highlight Bash shell scripts linenos%}
User.all.each do |user|
puts user.name
end
{% endhighlight %}
Việc lấy toàn bộ dữ liệu của table chỉ với 1 lần hit database như đoạn lệnh trên là không nên nếu như lượng dữ liệu là quá lớn.
ActiveRecord cung cấp 2 cách tìm kiếm theo batches như sau
find_each()

Lấy record theo từng batch và trả về từng record riêng biệt
{% highlight Bash shell scripts linenos%}
User.find_each(:start => 10, :batch_size => 10) do |user|
puts user.name
end
find_in_batches()
{% endhighlight %}
Lấy record theo từng batch và trả về toàn bộ batch dưới dạng mảng các record
{% highlight Bash shell scripts linenos%}
User.find_in_batches(:start => 10, :batch_size => 10) do |user_batch|
user_batch.each do |user|
puts user.name
end
end
{% endhighlight %}
find_each() và find_in_batches() có 2 options là :batch_size và :start.
:batch_size cho ta lựa chọn số lượng records cần lấy trong mỗi batch.
:start cho ta đặt ID đầu tiên của batch records cần lấy.
2 options này giúp ta có thể tạo ra nhiều workers xử lý cùng 1 công việc. Giả sử mỗi worker có thể xử lý 5000 records với những điểm bắt đầu riêng biệt.

### 2.where()

where() giúp ta lấy records theo điều kiện
{% highlight Bash shell scripts linenos%}
User.where(name: ["John","Titor"])
=> SELECT "users".* FROM "users" WHERE "users"."name" IN ('John', 'Titor')
{% endhighlight %}
### 3.group()/having()

group() và having() có cách sử dụng như GROUP BY và HAVING trong SQL
{% highlight Bash shell scripts linenos%}
User.limit(5).group('city').having('city = ?', 'Hanoi')
=> SELECT "users".* FROM "users" GROUP BY city HAVING city = 'Hanoi' LIMIT 5
{% endhighlight %}

### 4.order()/limit()

order() giúp ta lấy records từ database theo sắp xếp nhất định.
limit() giúp ta giới hạn số lượng records cần lấy ra.
{% highlight Bash shell scripts linenos%}
User.limit(3).order('name')
=> SELECT "users".* FROM "users" ORDER BY name LIMIT 3
{% endhighlight %}
### 5.select()

Theo mặc định, khi lấy records, kết quả trả về sẽ chứa toàn bộ các trường của bảng dữ liệu.
Khi sử dụng select(), kết quả trả về chỉ bao gồm các trường mà ta định ra trong select()
{% highlight Bash shell scripts linenos%}
User.limit(5).select('name, email')
=> SELECT name, email FROM "users" LIMIT 5
{% endhighlight %}

### 6.Vấn đề n+1 queries

{% highlight Bash shell scripts linenos%}
User.limit(3).each do |user|
puts user.microposts.first.content
end
{% endhighlight %}
Đoạn code trên khi chạy sẽ thực hiện 1 query (để lấy 3 users) + 3 queries (1 query cho mỗi user để lấy content của micropost) = 4 queries.

### a.includes()
Với includes(), ActiveRecords giúp ta load trước các associations sẽ được sử dụng trong query, làm giảm số lượng query cần thực hiện.
Khi ta thực hiện query trên các associations, vì dữ liệu đã được load sẵn nên không cần phải vào database lần nữa.
{% highlight Bash shell scripts linenos%}
User.limit(3).includes(:microposts).each do |user|
puts user.microposts.first.content
end
{% endhighlight %}
Đoạn code trên sẽ chỉ thực hiện 2 queries thay vì 4 queries như trước.
{% highlight Bash shell scripts linenos%}
SELECT "users".* FROM "users" LIMIT 3
SELECT "microposts".* FROM "microposts" WHERE "microposts"."user_id" IN (3, 4, 5)
{% endhighlight %}
Tuy nhiên khi sử dụng includes() cần chú ý về khối lượng dữ liệu được load sẵn. Nếu dữ liệu quá lớn thì sử dụng includes() là không nên.
Với lượng dữ liệu nhỏ ta có thể sử dụng joins().

### b.joins()

Để join các tables trong databases, ta có thể sử dụng joins()
{% highlight Bash shell scripts linenos%}
User.joins(:microposts)
=> SELECT "users".* FROM "users" INNER JOIN "microposts" ON "microposts"."user_id" = "users"."id"
{% endhighlight %}

