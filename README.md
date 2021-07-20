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
- Trái ngược với lập trình truyền thống, trong đó mã tùy chỉnh của chúng tôi thực hiện các lệnh gọi đến thư viện, IoC cho phép một khuôn khổ kiểm soát luồng chương trình và thực hiện các lệnh gọi đến mã tùy chỉnh của chúng tôi. Để kích hoạt điều này, các khung công tác sử dụng các phần trừu tượng với hành vi bổ sung được tích hợp sẵn. Nếu chúng ta muốn thêm hành vi của riêng mình, chúng ta cần mở rộng các lớp của khung công tác hoặc bổ sung các lớp của riêng chúng ta.