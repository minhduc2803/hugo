---
comments: true
image: post/image/concurrency-vs-parallelism/thumb-nail.jpg
title: "Concurrency vs. Parallelism"
date: 2020-08-04T01:51:24+07:00
slug: "concurrency-vs-parallelism"
---

"Concurrency is not Parallelism" là điều mà chúng ta sẽ làm rõ trong bài viết này.

Bạn không nghe nhầm đâu, "Concurrency is not Parallelism". Nhiều việc diễn ra "đồng thời" không nhất thiết phải diễn ra "song song" với nhau. Để làm rõ điều này có lẽ tôi phải giới thiệu thêm một thuật ngữ nữa, "simultaneous".

### Concurrency vs. Simultaneously

Cả hai từ trên khi dịch ra tiếng việt đều mang nghĩa là "đồng thời", trong tiếng anh cũng đều có nghĩa là "occurring at the same time". Nhưng thực sự 2 từ này có chút khác biệt, "Concurrency" dùng để nói tới các sự kiện diễn ra trong "một khoảng thời gian" còn "Simultaneous" mô tả các sự kiện diễn ra trong cùng "một thời điểm". 

Hai khái niệm sẽ rõ ràng hơn trong technology. Khi hệ điều hành đa nhiệm ra đời, CPU vẫn chỉ có một core nhưng vẫn có thể xử lý nhiều thread "concurrently", người dùng có thể vừa chơi game vừa lướt web mà không hề bị gián đoạn. Sự đồng thời này là "Concurrency", tức là trong một khoảng thời gian (vài giây chẳng hạn) web và game đều được CPU xử lý, nhưng không "Simultaneous", vì trong một thời điểm nhất định, CPU chỉ xử lý một thread nhất định, rồi sau đó rất nhanh luân phiên chuyển qua xử lý thread khác, được điều khiển bởi bộ định thời của hệ điều hành. Ví dụ như CPU điều khiển game trong 0.01s sau đó dừng, xử lý web 0.01s, rồi lại dừng, chuyển qua hiển thị game trong 0.01s,... Khiến cho trong một khoảng thời gian vài giây, 2 task game và web diễn ra đồng thời với nhau. Vì sự chuyển đổi của CPU diễn ra quá nhanh, nên việc hiển thị trở nên quá mượt mà khiến người dùng dễ lầm tưởng web và game chạy "song song" với nhau. 

### Concurrency is not Parallelism

    Nói như vậy không có nghĩa rằng mọi thứ song song thì không đồng thời, chỉ là điều ngược lại chưa chắc đã đúng.

![concurrency-vs-parallelism](/post/image/concurrency-vs-parallelism/concurrency-vs-parallelism.png)


Những sự kiện kiện diễn ra "parallel" khi chúng "simultaneously". Tức tại một thời điểm phải có ít nhất 2 sự kiện cùng diễn ra. Như vậy với hệ điều hành đa nhiệm 1 CPU one core, web và game không chạy "song song" với nhau. Nhưng chúng ta vẫn coi như chúng chạy "Concurrently". Muốn có "Parallelism" có lẽ chúng ta cần ít nhất 2 CPU hoặc 1 CPU 2 core. Như vậy 2 CPU có thể xử lý 2 task cùng một lúc, ý tôi là "Simultaneously".

Giống như ví dụ với hệ điều hành đa nhiệm ở trên, tượng tượng 2 chuỗi task công việc cho web và game là 2 hàng người đợi mua coffee, còn CPU là máy pha coffee. 

![coffee-line](/post/image/concurrency-vs-parallelism/coffee.png)

Nếu chỉ có một máy pha coffee thì chắc chắn tại một thời điểm chỉ một người được phục vụ, máy pha coffee sẽ luân phiên phục vụ từng người của mỗi hàng đợi, vậy cả 2 hàng người đều được phụ cùng một lúc => concurrency but not parallelism.

Còn nếu có 2 máy pha coffee, easy, mỗi máy sẽ phục vụ riêng một hàng người, tại một thời điểm sẽ có thể có 2 người được phục vụ => concurrency and parallelism



Yeah, kết luận là "concurrently is not parallelism". Một khái niệm mới mà cũ. Hi vọng bài viết ngắn này có thể làm rõ hơn khái niệm "concurrency"  và "parallelism", cùng với đó là "simultaneous" cho bạn đọc.

And now, thanks for reading ^^
