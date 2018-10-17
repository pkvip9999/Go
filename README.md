# Go


[Source](https://medium.com/exploring-code/why-should-you-learn-go-f607681fad65 "Permalink to Why should you learn Go? – Exploring Code – Medium")

# Tại sao nên học Go? – Exploring Code – Medium

Trong vài năm qua,1 ngôn ngữ lập trình mới đang nổi lên: Go hoặc GoLang. Không có gì làm cho developer trở nên điên rồ hơn một ngôn ngữ lập trình mới, đúng không? Vì vậy, tôi bắt đầu học Go trước 4 đến 5 tháng và ở đây tôi sẽ cho bạn biết lý do tại sao bạn cũng nên học ngôn ngữ mới này.

Tôi sẽ không dạy bạn, cách bạn có thể viết “Hello World !!” trong bài viết này. Có rất nhiều bài báo online cho điều đó. Tôi sẽ giải thích giai đoạn hiện tại của phần mềm máy tính và tại sao chúng ta cần ngôn ngữ mới như Go? Bởi vì nếu không có vấn đề gì thì chúng ta không cần giải pháp, đúng không?
### **Giới hạn về phần cứng:**
Bộ xử lý Pentium 4 đầu tiên với tốc độ xung nhịp 3.0GHz đã được Intel giới thiệu vào năm 2004. Hiện giờ, Mackbook Pro 2016 của tôi có tốc độ xung nhịp 2,9GHz. Vì vậy, gần một thập kỷ, không có quá nhiều lợi ích trong việc tăng sức mạnh xử lý . Bạn có thể thấy so sánh việc tăng sức mạnh xử lý với thời gian biểu đồ bên dưới

Từ biểu đồ trên, bạn có thể thấy rằng hiệu suất của một luồng đơn và tần số của bộ xử lý vẫn ổn định trong gần một thập kỷ. Nếu bạn đang nghĩ rằng việc thêm nhiều transistor là giải pháp, thì bạn đã sai. Điều này là do ở quy mô nhỏ hơn, một số tính chất lượng tử bắt đầu nổi lên (như đường hầm) và vì nó thực sự tốn nhiều tiền hơn để đặt nhiều transistor hơn (tại sao?) Và số transistor bạn có thể thêm vào mỗi đô la bắt đầu giảm.

Vì vậy, để giải quyết vấn đề trên,
  - Các nhà sản xuất bắt đầu bổ sung thêm nhiều nhân hơn cho bộ vi xử lý. Ngày nay chúng tôi có sẵn các CPU 4 nhân và 8 nhân 
  - Chúng tôi cũng giới thiệu về siêu luồng.
  - Đã thêm bộ nhớ cache vào bộ xử lý để tăng hiệu suất
  
  Nhưng các giải pháp trên cũng có những hạn chế riêng. Chúng tôi không thể thêm nhiều bộ nhớ đệm và nhiều hơn nữa để bộ xử lý tăng hiệu suất như bộ nhớ đệm có giới hạn vật lý: bộ nhớ cache càng lớn, nó càng chậm. Thêm nhiều nhân hơn cho bộ vi xử lý cũng có chi phí của nó. Ngoài ra, điều đó không thể mở rộng đến vô thời hạn. Các bộ vi xử lý đa nhân này có thể chạy đồng thời nhiều luồng và mang lại sự đồng thời về hình ảnh. Chúng ta sẽ thảo luận sau.
  
Vì vậy, nếu chúng ta không thể dựa vào những cải tiến phần cứng, cách duy nhất để đi là phần mềm hiệu quả hơn để tăng hiệu suất. Nhưng thật đáng buồn, ngôn ngữ lập trình hiện đại không hiệu quả lắm.

  > “Bộ vi xử lý hiện đại giống như những chiếc xe hơi vui nhộn chạy bằng nitro, chúng vượt trội trong một phần tư dặm. Thật không may là các ngôn ngữ lập trình hiện đại giống như Monte Carlo, chúng có đầy đủ các vòng xoắn và quay. ”- David Ungar


### **Go có goroutines !!**

Như chúng ta đã bàn ở trên, những nhà chế tạo phần cứng  ngày càng thêm nhiều core vào bộ xử lý để cải thiện hiệu năng. Tất cả các trung tâm dữ liệu đều chạy trên những con xử lý này và chúng ta nên tăng số lượng core trong vài năm tới. Hơn nữa, các ứng dụng ngày nay đều sử dụng nhiều micro-service để duy trì kết nối cơ sở dữ liệu, message queue và duy trì cache. Vì vậy, các phần mềm mà chúng ta thiết kế và các ngôn ngữ lập trình nên hỗ trợ concurrency dễ dàng hơn và chúng có thể được mở rộng bằng cách tăng số lượng core.

Nhưng hầu hết các ngôn ngữ lập trình hiện đại (như Java, Python vân vân) đều từ những môi trương đơn luồng những năm 90. Hầu hết những ngôn ngữ lập trình đó đều hỗ trợ đa luồng. Nhưng vấn đề thực sự là khi thực thi concurrent, threading-looking, race condition và deadlock. ** ** Những thứ này khiến việc tạo các ứng dụng đa luồng trên những ngôn ngữ này trở nên khó khăn.

Ví dụ, tạo 1 luồng mới trong Jave không thực sự hiệu quả về mặt bộ nhớ. Vì mỗi 1 luồng tiêu tốn khoảng 1MB kích thước bộ nhớ heap và thậm chí nếu bạn bắt đầu  chạy hàng nghìn luồng, sẽ gây áp lực rất lớn trên bộ nhớ heap và gây ra shut down vì tràn bộ nhớ. Cũng như là nếu bạn muốn giao tiếp giữa 2 hoặc nhiều luồng, điều này là rất khó khăn.

Mặt khác, Go được released trong năm 2009 khi các bộ xử lý nhiều-core đã xuất heienj. Đó là lý do Go được xây dựng gắn liền với concurrency. Go có goroutines thay vì các luồng. Nó tiêu thụ khoảng 2KB bộ nhớ từ heap. Vì vậy, bạn có thể chạy hàng triệu goroutines cùng lúc.
![][1]

 Goroutines hoạt động thế nào? Reffrance: 

**Các lợi ích khác như :**

* Goroutines có segmented stacks có khả năng mở rộng. Điều này có nghĩa là chúng sẽ chỉ sử dụng thêm bộ nhớ khi cần thiết .
* Goroutines có thời gian startup nhanh hơn threads.
* Goroutines come with built-in primitives để giao tiếp an toàn giữa chúng (channels).
* Goroutines cho phép tránh các phương pháp mutex locking khi chia sẽ các cấu trúc dữ liệu.
* Ngoài ra, goroutines và OS threads không có 1:1 mapping. 1 goroutine đơn có thể chạy trên đa luồng. Goroutine được ghép vào 1 lượng nhỏ các luồng OS.


> Bạn có thể xem Rob Pike's excellent talk [concurrency không phải là parallelism][2]  để hiểu sâu hơn về vấn đề này.

Tất cả các điểm trên khiến Go trở nên mạnh mẽ trong xử lý concurrency như Java, C và C++ trong khi vấn giữ được các tư tưởng và vẻ đẹp của code thực thi concurrency  như Erlang.

![][3]

Go có những thứ tốt đẹp nhất của cả 2 bên. Dễ dàng để viết các concurrent và  quản lý các concurrent.

## Go chạy trực tiếp trên nền tảng phần cứng

1 trong những lợi thế rõ rệt nhất của việc sử dụng C, C++ với các ngôn ngữ bậc cao hiện đại khác như Java/Python và hiệu năng của nó. Vì C/C++ được biên dịch chứ không phải thông dịch.

Các bộ xử lý hiểu mã nhị phân. Thông thường, khi bạn build 1 ứng dụng sử dụng Java hay các ngôn ngữ trên nền JVM khác khi bạn biên dịch project của mình, nó sẽ biên dịch code mà con người đọc được thành byte-code mà có thể hiểu bởi JVM hay các máy ảo khác chạy trên cùng của  của nền tảng Ó. Trong khi thực thi,  VM sẽ phiên dịch byteoode đó và chuyển chúng thành mã nhị phân mà bộ xử lý có thể hiểu được

Trong khi đó, C/C++ không thực thi trên các VMs và chúng loại bỏ 1 bước từ chu trình thực thi để tăng hiệu năng. Nó trực tiếp biên dịch code tự nhiên thành mã nhị phân

Nhưng, giải phóng và phân bổ biến trong những ngôn ngữ đó lại rất khó khăn. Trong khi hầu hết các ngôn ngữ lập trình xử lý phân bổ đối tượng và loại bỏ bằng cách sử dụng Garbage Collector hoặc thuật toán Reference Counting.

Go kết hợp những điều tốt nhất của cả 2 loại. Giống như những ngôn ngữ bậc thấp như C/C+++, Go là ngôn ngữ biên dịch. Điều này có nghĩa là hiệu năng sẽ hầu như  giống với các ngôn ngữ bậc thấp. Nó cũng sử dụng garbage collection để phân bổ và loại bỏ các đối tượng. Vì vậy sẽ không có các lệnh như malloc() và free(). Tuyệt vời!


## Code viết bằng Go dễ bảo trì.
Để tôi nói cho bạn biết 1 điều. Go không ó những cú pháp lập trình diên dồ như các ngôn ngữ khác có. Nó sử dụng ngữ pháp ngắn  gọn và khéo léo.

Các nhà thiết kế Go tại Google luôn tâm niệm điều này trong tâm trí khi họ tạo ra ngôn ngữ này. Vì google có code base rất lớn và hàng ngàn lập trình viên đang làm việc trên cùng code-base, code nên dễ hiểu với những lập trình viên khác và 1 phần code nên có tối thiểu ảnh hưởng phụ với các phần code khác. Điều này khiến code dễ bảo  trì và chỉnh sửa.

Go chủ định loại bỏ nhiều tính năng của các ngôn ngữ OOP hiện đại.

- Không lớp. Mọi thứ được chia thành các package thôi. Go chỉ có struct hay cho các classs
- Không hỗ trợ  kế thừa. Điều này sẽ khiến code dễ chỉnh sửa. Trong các ngôn ngữ khác như Java/Python, néu class ABC kế thưuaf class XYZ và bạn có 1 vài thay đổi tỏng class XYZ, điều này có thể gây nên 1 vài ảnh hưởng với các lớp khác kế thừa XYZ. Bằng cách bỏ đi kế thừa, Go khiến việc hiểu code dễ hiểu hơn (vì không có super class để xem khi nhìn 1 phần code).
- KHông constructoe
- Không annotations
- Không generics
- KHông exception

Những thay đổi trên khiến Go thực sự kh biệt với các ngôn ngữ khác và nó khiến việc lập trình bằng Go khác biệt với những ngôn ngữ khác. Bạn có thể không thích 1  vài thứ bên trên. Nhưng nó không giống việc bạn không thể code ứng dụng với những tính năng trên. Tất cả những gì bạn phải làm là viết thêm 2-3 dòng. Nhưng về mặt tichs cực, nó sẽ khiến code sáng sủa hơn và code thêm nuột

Biểu đồ trên hiển thị Go hiệu quả tương đương với C/C++, trong khi cú pháp code đơn giản như Ruby Python và các ngôn ngữ khác. Điều lại thuận lợi cho cả con người và các trình xử lý.

Không giống như các ngôn ngữ khác như Swift, cú pháp của Go rất ổn định. Nó vẫn vậy kể từ lần realease public lần đầu 1.0, từ năm 2012. Điều này khiến nó tương thích qua khác phiên bản.

Go được Goolge đưng sau.
Tôi biết điều này không thực sự là 1 lợi thế kĩ thuật. Nhưng Go được thiết kế và hỗ trợ bởi Google. Google có 1  trong những cơ sở hạ tầng cloud lớn nhất thế giới và nó có khả năng mở rộng lớn. Go được thiết kế bởi Google để giải quyết các vấn đề của họ về hỗ trợ khả năng mở rộng và hiệu quả. Đó là những vấn đề tương tự bạn sẽ phải đối mặt trong khi tạo ra các máy chủ của riêng bạn.

## Phần kết luận:

Mặc dù Go rất khác với các ngôn ngữ hướng đối tượng khác, nó vẫn là cùng một loại. Go cung cấp cho bạn hiệu suất cao như C / C ++, xử lý đồng thời siêu hiệu quả như Java và thú vị với mã như Python / Perl.

Nếu bạn không có bất kỳ kế hoạch học Go, tôi vẫn sẽ nói giới hạn phần cứng đặt áp lực cho chúng tôi, các nhà phát triển phần mềm để viết mã siêu hiệu quả. Nhà phát triển cần hiểu phần cứng và làm cho chương trình của họ tối ưu hóa phù hợp. Phần mềm được tối ưu hóa có thể chạy trên phần cứng rẻ hơn và chậm hơn (như thiết bị IOT) và tác động tổng thể tốt hơn đến trải nghiệm người dùng cuối.



[1]: https://cdn-images-1.medium.com/max/1600/1*NFojvbkdRkxz0ZDbu4ysNA.jpeg
[2]: https://blog.golang.org/concurrency-is-not-parallelism
[3]: https://cdn-images-1.medium.com/max/1600/1*xbsHBQJReC5l_VO4XgNSIQ.png

  
