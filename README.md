# Tra_loi_cau_hoi_Spring

1. Vẽ và trình bày cách Spring MVC xử lý request

- Request được gửi đến sẽ được nhận và phân loại bởi Front controller, sau đấy nó được gửi đến các Controller tương ứng
  để xử lý.
- Controller create model nếu cần và gửi model về lại cho Front controller, Front controller gửi model đấy cho View
  template tương ứng để render response.
- View template gửi lại response đã được render cho Front controller để nó trả response về cho client.
  <Sơ đồ Spring MVC xử lý request - Hình 1>

2. Trình bày cơ chế Dependency Injection

- Dependency Injection là một design pattern được sử dụng để triển khai IoC, trong đó quyền điều khiên được đảo ngược
  thiết lập trong object phụ thuộc.
- Việc kết nối đối tượng với các đối tượng khác, hoặc "ịnject" đối tượng vào các đối tượng khác, được thực hiện bởi một
  trình lắp ráp chứ không phải bởi chính các đối tượng.

- Ví dụ không sử dụng DI:
  public class Store { 
    private Item item;

    public Store() { 
      item = new ItemImpl1();    
    } 
  }

- Sử dụng DI:
  public class Store { 
    private Item item; 
    public Store(Item item) { 
      this.item = item;
    }
  }
  
3. Có bao nhiêu cách để thực hiện Dependency Injection? Trình bày?
- Có 3 cách đẻ thực hiện DI: constructors, setters or fields.
- Constructors:
  Container sẽ gọi một phương thức khởi tạo với các đối số đại diện cho một dependencies mà chúng ta muốn đặt.
  @Configuration
  public class AppConfig {

  @Bean
  public Item item1() {
  return new ItemImpl1();
  }

  @Bean
  public Store store() {
  return new Store(item1());
  }
  }
  
- Setters:
  Container sẽ gọi các phương thức setter của lớp sau khi gọi phương thức khởi tạo không tham số để khởi tạo bean.
  @Bean
  public Store store() {
  Store store = new Store();
  store.setItem(item1());
  return store;
  }
  
- Fields:
  Chúng ta có thể đưa các phần phụ thuộc vào bằng cách đánh dấu chúng bằng chú thích @Autowired. Trong khi khởi tạo đối tượng Store, nếu không có phương thức khởi tạo hoặc setter nào của Item được đánh dấu bean, container sẽ sử dụng reflection để tìm constructor rồi khởi Item và đưa vào Store.
  public class Store {
    @Autowired
    private Item item;
  }
  
4. Framework là gì ? Framework khác Library chỗ nào ?
- Framework là ứng dụng phần mềm có tính trừu tượng.
- Framework cung cấp các tính năng chung , thông dụng có thể tùy biến để tạo nên các ứng dụng khác nhau.
- Framework:
  • Framework là một bộ khung mà code của mình đắp phần thịt lên.
  • Framework call your code.
  • Framework contain library.
- Library:
  • Library thực hiện các hành động cụ thể, đã xác định rõ ràng.
  • Your code call library.
- Sự khác biệt rõ ràng nhất là đến từ IoC.

5. Spring Framework là gì ?
- Spring là framework nhẹ với mã nguồn mở giúp đơn giản hóa đáng kể việc phát triển các ứng dụng doanh nghiệp trên java.

6. Lợi ích của Spring Framework?
- Spring cung cấp một bộ API phong phú được xây dựng trên Java Servlet, JDBC, transaction, webservices, ... giúp công việc của lập trình viên trở nên dễ dàng hơn.

7. Nguyên lý đảo ngược quyền điều khiển (Inversion of Control) là gì ?
- Inversion of Control là một nguyên tắc trong kỹ thuật phần mềm để chuyển quyền kiểm soát các đối tượng hoặc các phần của chương trình sang một container hoặc framework,nó thường được sử dụng nhất trong lập trình hướng đối tượng.

8. Giải thích IoC? Lợi ích của IoC ?
- Trái ngược với lập trình truyền thống, trong đó code của chúng ta thực hiện các lệnh gọi đến library, IoC cho phép một framework kiểm soát luồng chương trình và thực hiện các lệnh gọi đến code của chúng ta. Để làm được điều này, các framework sử dụng các phần trừu tượng hóa với hành vi được tích hợp sẵn. Nếu chúng ta muốn thêm hành vi của riêng mình, chúng ta cần extends các lớp của framework hoặc bổ sung các lớp của riêng mình.
- Lợi ích của IoC:
  • Tách việc thực thi một Task khỏi việc triển khai nó.
  • Giúp chuyển đổi giữa các cách implements khác nhau dễ dàng hơn.
  • Chương trình có tính module hơn.
  • Dễ dàng hơn trong việc test bằng cách cô lập từng phần.
  
9. Bean là gì?
- Trong Spring, các đối tượng tạo thành xương sống của ứng dụng của bạn và được quản lý bởi Spring IoC container được gọi là bean. Bean là một đối tượng được khởi tạo, lắp ráp và quản lý bởi một container Spring IoC.

10. Trong Spring có bao nhiêu Bean Scope?
- Trong Spring cos 5 Bean Scope.

11. @Autowire là gì?
- Autowire của Spring framework cho phép đưa dependency vào đối tượng một cách ngầm định. Bên trong nó sử dụng setter hoặc constructor để inject.

12. @Component có ý nghĩa gì?
- @Component là một chú thích cho phép Spring tự động phát hiện các bean tùy chỉnh của chúng ta. Nói cách khác, mà không cần phải viết code rõ rằng, Spring sẽ: Quét ứng dụng để tìm các lớp được chú thích bằng @Component khởi tạo chúng và đưa dependency được chỉ định vào chúng.

13. Trình bày ý nghĩa của Controller
- Controller là nơi nhận request từ người dùng, xử lý request, xây dựng model với dữ liệu và chọn view để trả lại kết quả của cho người dùng.

14. Trình bày ý nghĩa của ModelAndView Interface
-  Giữ cả Model và View. Interface này chỉ giữ cả hai để giúp controller có thể trả về cả model và view trong một return duy nhất.

15. Trình bày ý nghĩa của ModelMap Interface
- ModelMap được sử dụng để chuyển các giá trị để hiển thị trên View. Ưu điểm của ModelMap là nó cho chúng ta khả năng truyền một collection các giá trị và xử lý các giá trị này như thể chúng nằm trong một Map.

16. Trình bày ý nghĩa của ViewResolver Interface
- ViewResolver cung cấp ánh xạ giữa View name và View thực tế (gọi view name để chỉ đến view đấy).

17. Định nghĩa URI với các phương thức khác nhau như GET, POST, PUT, PATH, DELETE
- GET: Để lấy dữ liệu từ server theo uri đã gửi.
- POST: Gửi thông tin tới server và thường dùng để lưu thông tin vào server.
- PUT: Để câp nhật thông tin của dữ liệu trong server, nếu chỉ update 1 phần thì các phần còn lại là null.
- PATCH:Để câp nhật thông tin của dữ liệu trong server, nếu chỉ update 1 phần thì các phần còn lại giữ nguyên.
- DELETE: Xóa dữ liệu trong server.

18. Phân biệt POST với GET
- GET : gửi dữ liệu lên server thông qua URL, thông tin hiển thị lên url, kích thước url giới hạn.
- POST : gửi dữ liệu lên server dưới dạng ẩn, không hiển thị param lên url, dữ liệu không giới hạn. 
– Get thực thi nhanh hơn Post vì cơ chế:
  • Post : các tham số được đóng gói vào 1 file tạm, sau đó trình duyệt gửi file tạm đó lên server và server lưu lại file tạm đó sau đó mới phân tích.
  • Get : đưa chuỗi string lên URL, server tách chuỗi lấy được tham số.
  
19. Phân biệt POST với PUT
- POST là để thêm mới dữ liệu (id được tạo tự động), PUT là để sửa dữ liệu (tự thêm id nếu dùng PUT có thể dẫn đến lỗi).

20. Thao tác với form trong ứng dụng Spring MVC
- SpringMVC cung cấp các thẻ trong thư viện spring-form.tld để thao tác với form.
- spring-form.tld cung cấp thẻ form và các thẻ thành phần khác để thao tác với form.

21. @RequestMapping làm gì?
- Annotation @RequestMapping được sử dụng để ánh xạ các request tới các action tương ứng của controller

22. Trình bày cơ chế Data Binding
- Data binding của Spring cho phép input của người dùng được liên kết động với các bean. Nói cách khác, nó cho phép thiết lập các giá trị thuộc tính vào một đối tượng đích. Lớp DataBinder cung cấp chức năng này.

23. Thuộc tính consumes trong các Request Mapping là gì ?
- Thuộc tính consumes để ánh xạ đến Content-Type của request.

24. Data Binding là gì?
- DataBinding là cơ chế liên kết dữ liệu đầu vào (hoặc đầu ra) với các đối tượng model, giúp cho việc tươngtác với dữ liệu trở nên dễ dàng.

25. Formatter là gì ? Converter là gì ?
- Spring Converter là một đối tượng được dùng để chuyển đổi kiểu dữ liệu này sang kiểu dữ liệu khác. Chẳng hạn, chúng ta có thể biểu diễn cùng một ngày theo những định dạng khác nhau, chẳng hạn như: “December 25, 2016,” 12/25/2016,” “2016-12-25”.
- Formatter cũng hoạt động giống như converter, tức là chuyển đổi một kiểu dữ liệu sang kiểu dữ liệu khác. Tuy nhiên, kiểu dữ liệu nguồn của Formatter là String, trong khi đó converter có thể làm việc với bất cứ kiểu dữ liệu nguồn nào.

26. ORM là gì?
- ORM (Object-Relational Mapping) là kỹ thuật liên kết giữa các đối tượng trong lập trình với các đối tượng trong CSDL.

27. JPA là gì? Spring Data JPA là gì?
- JPA là một đặc tả của Java cho APIs truy cập vào các DB dùng SQL khác nhau.
- Spring Data JPA là một sub-project của Spring Data, cung cấp abstraction layer sử dụng JPA với implement mặc định là Hibernate.

28. Hibernate là gì? Hibernate làm gì với database?
- Hibernate là một thư viện ORM (Object Relational Mapping) mã nguồn mở giúp lập trình viên viết ứng dụng Java có thể map các objects (pojo) với hệ quản trị cơ sở dữ liệu quan hệ, và hỗ trợ thực hiện các khái niệm lập trình hướng đối tượng với cớ dữ liệu quan hệ.
- Hibernate giúp lưu trữ và truy vấn dữ liệu quan hệ mạnh mẽ và nhanh. Hibernate cho phép bạn truy vẫn dữ liệu thông qua Java Persistence API (JPA) hoặc bằng ngôn ngữ SQL mở rộng của Hibernate (HQL) hoặc bằng SQL thuần (Native SQL).

29. Liệt kê một số annotation của Hibernate.
- @Entity Annotation: Đánh dấu class là một entity.
- @Table Annotation: Xác định các chi tiết của bảng như tên, ràng buộc, schema, catalogue.
- @Id Annotation: Đánh dấu id của bảng.
- @GeneratedValue Annotation: Giá trị của field được tự động generate với 2 tham số là strategy và generator.
- @Column Annotation: Xác định chi tiết column được map đến, gồm các thuộc tính về tên, độ dài, nullable, unique.

30. Entity là gì?
- Một Entity đại diện cho một bảng trong cơ sở dữ liệu quan hệ và mỗi field trong thực thể tương ứng với một hàng trong bảng đó.

31. Persistence Context và Entity Manager là gì?
- Persistence Context là tập các thể hiện của entity được quản lý,tồn tại trong một kho dữ liệu.
- Entity Manager là interface để quản lý, tương tác với Persistence Context: tạo hoặc xóa thể hiện của entity, tìm kiếm entity theo khóa chính, thực thi lệnh truy vấn lên entity.

32. Câu lệnh truy vấn động, câu lệnh truy vấn tĩnh là gì?
- Dynamic query là câu lệnh sẽ được biên dịch trong lúc runtime -> sử dụng trong các trường hợp cần query đến từ người dùng.
- Static query là câu lệnh được biên dịch lúc compile -> sử dụng cho các truy vấn cố định, không thay đổi vì nó k thay đổi khi runtime.

33. Trạng thái của Entity bao gồm những gì?
- Transient: Một object vừa mới được tạo ra mà chưa được kết nối với Hibernate và cũng chưa được ánh xạ vào bất cứ bảng nào trong database thì sẽ được coi như là ở trạng thái New (Transient).
- Persistent: Thực thể Persistent đã được ánh xạ vào trong database và được quản bị bởi Persistence Context đang hoạt động. Bất cứ thay đổi nào tác động lên entity sẽ được ghi nhận và  cuồi cùng được ghi ổn định vào trong cơ sở dữ liệu trong lệnh Session flush.
- Detached: Một khi Persistence Context đang chạy đã đóng lại, mọi entity được liên kết trước đó sẽ bị tách ra. Các thay đổi tiếp theo sau đó sẽ không còn được theo dõi và động bộ hóa vào trong database nữa.
- Deleted: Bị xóa.

34. Có bao nhiêu loại mapping trong Hibernate?
- Có 4 loại mapping trong Hibernate:
  • Many to One.
  • One to Many.
  • One to One.
  • Many to Many.


35. SessionFactory là gì?
- SessionFactory là một interface ở trong org.hibernate package nó extends Referenceable and Serializable interface và cung cấp factory methods để tạo ra session object.


36. Liệt kê ba trạng thái của đối tượng trong Hibernate.
- Transient: Các đối tượng transient (không ổn định) là những “đối tượng lẻ” - vừa được tạo và chưa được phân biệt bởi một Phiên cụ thể.
- Persistent: Các đối tượng persistent (liên tục) là những đối tượng đang mở - chúng xảy ra bất cứ khi nào bạn lưu hoặc truy xuất một số trường hợp nhất định từ cơ sở dữ liệu Hibernate.
- Detached: Các đối tượng trở nên detached (tách rời) sau khi phiên được đóng bởi nhà phát triển.

37. Validation dữ liệu là gì?
-  Data validation là việc kiểm tra dữ liệu trước khi xử lý nhằm đảm bảo dữ liệu đáp ứng các yêu cầu đặt ra.

38. Trình bày cách triển khai validate dữ liệu trong Spring.
- Sử dụng các annotation để validate data trong class entity, khi kiểm tra sử dụng annotation @valid hoặc @validated kết hợp bindingResult để kiểm tra.

39. Binding Result là gì?
- BindingResult là đối tượng của Spring mà giữ kết quả xác thực và ràng buộc và chứa các lỗi có thể xảy ra. BindingResult phải đến ngay sau khi đối tượng mô hình được xác thực nếu không Spring sẽ không xác thực đối tượng và ném ngoại lệ.

40. AOP là gì? AOP gồm những yếu tố nào?

41. Các loại Advice.

42. JoinPoint là gì?

43. Nếu cách ban triển khai AOP mà bạn dùng trong dự án.
- Khai báo các dependency Spring-AOP, aspectj.
- Triển khai class AOP vs annotation aspect, sử dụng các annotation khác để weave các method trong aspect theo ý muốn.

44. Xử lý ngoại lệ trong Spring MVC như thế nào?
