---


---

<h1 id="solid-prensiplerine-basic-örnekler">SOLID Prensipleri'ne Basic Örnekler</h1>
<p>SOLİD Prensipleri, 2000 yılında Robert C. Martin'in yazdığı <a href="https://fi.ort.edu.uy/innovaportal/file/2032/1/design_principles.pdf"><em>Design Principles and Design Patterns</em></a> makalesinde <em>Principles of Object Oriented Class Design</em> bölümünün ilk 5 maddesi, aynı zamanda nesneye yönelik programlamanın da temel prensipleri olarak kabul edilerek yazılım üretimindeki bütün alışkanlıkları değiştirdi.</p>
<p>Prensiplerin baş harflerinden oluşan ve Martin'e ait bu kavramsallaştırma; sürdürülebilir, anlaşılabilir, esnek ve yazılım büyüdükçe karmaşanın artmasını engellemeyi temel alan ilkelerden oluşmaktadır.</p>
<p>Binlerce tez, makale konusu oldu bu sebeple belirtmek gerek- genelde baştan beklentiyi düşürmek devamında yazarken de bir rahatlama sağlar- ben de bir çaylak olarak en doğru örnekleri veremesem de en azından bu prensipleri kavrayış biçimimi yansıtması adına bu ilkelere basit tanımlamalar yaparak kodsuz biçimde sade örneklendirmeler yapmaya çalışacağım.</p>
<h3 id="single-responsibility-principle-tek-sorumluluk-prensibi">Single-Responsibility Principle (Tek Sorumluluk Prensibi)</h3>
<p>Bu prensip bir yazılım içerisinde görevlerin bölüştürülmesini her bir görev ayrı bir sınıfta tanımlanmasını esas alıyor. Aynı sınıf içerisinde birden fazla görev tanımlanmasının daha sonra o yazılımın geliştirilebilirliği, güncelliği açısından esnekliğine ket vuran bir structure biçimi olarak tanımlarken, ayrı ayrı görevler vermenin daha sonraki geliştirmeler sırasında karmaşayı engelleyen bir olanak sunduğunu söylüyor.</p>
<p>Örneğin, Class yapısıyla bir hesap makinası yapmak istiyorsunuz. Daha sonra ileri düzeyde işlemler ekleme gibi bir ihtimal de var. Aynı class içerisinde girilen sayıları çarpmanın yanında bir de o sayıların ortalamasını da aldırıyorsanız bu prensibe uymayan bir kod yazmış oluyorsunuz. Ancak toplama, ortalama alma, ekrana yazdırma vs gibi işleri ayrı classlarda tanımlarsanız bunlara yenilerini eklemeniz veya bazılarını çıkarmanız çok daha kolay hale geliyor.</p>
<h3 id="open-closed-principle-açık-kapalı-prensibi">Open-Closed Principle (Açık-Kapalı Prensibi)</h3>
<p>Open-closed principle, bir class yazıldığında onun modifiye edilmesinin hata(bug) yaşanmasına olanak sağlayacağından, modifiye etmeye kapalı genişletmeye veya geliştirmeye açık olmasını söyleyen prensiptir. Buna göre genişletme veya geliştirme yapılması istendiğinde classı extend ederek inherit ve abstract yapılar kullanılabilir.</p>
<p>Örneğin, bir kitapçıda edebiyat bölümünde en çok satılan kitabın ismini ve stok bilgisini yazdırmak istiyorsunuz. En çok satılan kitabı buldunuz. Yine aynı hesaplama yöntemiyle araştırma-inceleme bölümünde en çok satan kitabı bulmak istiyorsunuz. Bu noktada diğer classa bir extend açmanız gerekmektedir. Bu sayede hem bir önceki classa erişim sağlayıp istediğiniz zaman çok yüklenip istediğiniz zaman etkisiz kılıyorsunuz, hem de onun yapısını bozmamış oluyorsunuz.</p>
<h3 id="liskov-substitution-principle--liskovun-yerine-geçme-prensibi">Liskov Substitution Principle ( Liskov'un Yerine geçme Prensibi)</h3>
<p>Bu prensip ismini 1987'de 'Data abstraction' isimli makalesini yayınlayan Barbara Liskov'dan alıyor. Liskov'un bu makalede ise yaygın olarak bilinen tezi şu şekildedir;</p>
<p><code>Let Φ(x) be a property provable about objects x of type T. Then Φ(y) should be true for objects y of type S where S is a subtype of T.</code></p>
<p>Yani A sınıfı B sınıfının bir alt nesnesiyse bu ikisi programın davranışını bozmadan yer değiştirebilmelidir. <a href="https://www.baeldung.com/solid-principles">*</a></p>
<p>Bu da alt sınıflarınızın nesnelerinin üst sınıfınızdaki nesnelerle aynı şekilde davranmasını gerektirir. Yani türetilmiş nesneler arasında bir inputlar ve kurallar açısında bir uyum elastikiyet sağlayabilir ve program bu türetilmiş nesneleri <em>içerip aşarak</em> daha ileri kontroller yapabilir.</p>
<p>Bir alıntı:</p>
<p>"Alt seviye sınıflardan oluşan nesnelerin/sınıfların, ana(üst) sınıfın nesneleri ile yer değiştirdikleri zaman, aynı davranışı sergilemesi gerekmektedir. Türetilen sınıflar, türeyen sınıfların tüm özelliklerini kullanabilmelidir." <a href="https://medium.com/@gokhana/liskov-substitution-prensibi-nedir-kod-%C3%B6rne%C4%9Fiyle-soli%CC%87d-3cfc1cd63c1a">**</a></p>
<p>Açıkçası kimi ingilizce kaynaklardan mantığını biraz olsun kavramak daha mümkün ama tekrar kelimelere döküp basitleştirmek çok ciddi bir iş.</p>
<p>Bu prensipteki örneğini bahsettiğim ingilizce kaynaklardan birinde gördüğüm ve çok hoşuma giden bir basit uygulamayla vermeye çalışacağım. Kendim bu kadar güzel anlatan bir örnek veremem dolayısıyla bunu paylaşmak istedim.</p>
<p>Burada LSP için basitten başlayan ve ilerleyen bir kahve demleme makinası kodu örnek veriliyor. brewCoffee ve addCoffee methodlarını türeterek önce basic sonra da premium bir kahve makinası yapıyor. <a href="https://stackify.com/solid-design-liskov-substitution-principle/#:~:text=The%20Liskov%20Substitution%20Principle%20in,the%20objects%20of%20your%20superclass.">***</a></p>
<p><img src="http://image.prntscr.com/image/gzsIeWheRT_vHWmnn7ybWg.png" alt="s8"></p>
<h3 id="interface-segregation-principle--arayüz-ayrımı-prensibi">Interface Segregation Principle ( Arayüz Ayrımı Prensibi)</h3>
<p>Bir uygulamada kullanım açısında gerekli olmayan eklentilerin uygulamaya eklenmemesi gerektiğini söyleyen prensiptir. SOLID'deki 'I' arayüz anlamına gelir ve büyük interfacelerin küçük parçalara bölünmesini gerektirir. Bu sayede implement classlar küçük interface'de spesifik görevlerine odaklanması sağlanır. <a href="https://www.baeldung.com/solid-principles">*</a></p>
<p>Örneğin, hayvanların özelliklerini belirten bir interface kullanılsın.</p>
<p><code>public interface Animal {</code><br>
<code>void swim();</code></p>
<p><code>void run();</code></p>
<p><code>void eat();</code><br>
<code>}</code></p>
<p>Balıklar yemek yer ve sürünür ancak koşamaz. Burada balık ve köpek ayrımını yapmak için interface yapısı devreye giriyor ve implementasyon ile ayrı ayrı alanlar oluştururak her görev kendi alanına odaklanmış oluyor. Daha ilerisi için <a href="https://medium.com/@gokhana/interface-segregation-prensibi-nedir-kod-%C3%B6rne%C4%9Fiyle-soli%CC%87d-ac0fd6812ecf">****</a></p>
<h3 id="dependency-inversion-principle-bağımlılıkların-terslenmesi-prensibi">Dependency Inversion Principle (Bağımlılıkların Terslenmesi Prensibi)</h3>
<p>Bu prensibe göre, bir sınıfın, metodun ya da özelliğin, onu kullanan diğer sınıflara karşı olan bağımlılığı en aza indirgenmelidir. Bir alt sınıfta yapılan değişiklikler üst sınıfları etkilememelidir. <a href="https://medium.com/@gokhana/dependency-inversion-prensibi-nedir-kod-%C3%B6rne%C4%9Fiyle-soli%CC%87d-b61296523565">*****</a></p>
<p>Burada düşük seviyeli sınıflar ile yüksek seviyeli sınıfların birbirine bağlı olması ve birbirinden etkilenebilir olması prensibi ihlal edebilir. Bir sınıf yapısı başka bir yüksek seviyeli sınıfa tamamen bağlı ise eğer gelecekte çıkacak yeni bir güncellemede bu bağımlılık bütün altyapınızı değiştirmenize neden olabilir. Bu durumda Loosely Coupling yaklaşımı, SRP ilkesini ve ISP ilkesini bir araya getirerek interface içerisinde implement etmek gereklidir.</p>
<p>Örneğin, mail ve sms gönderen düşük seviyeli sınıflar notification sınıfı içerisine alınıyor ve notification gibi yüksek seviyeli bir sınıf sms ve email sınıflarına bağımlı hale geliyor. Buradan sonra ise message interface ile soyutlanıyor, bağımlı iki düşük seviyeli sınıf birbirine implement ediliyor ve notification bu soyutlama üzerinden yazılarak bağımlılıklarından kurtarılıyor. Detaylı örneği burada bulabilirsiniz. <a href="https://medium.com/@gokhana/dependency-inversion-prensibi-nedir-kod-%C3%B6rne%C4%9Fiyle-soli%CC%87d-b61296523565">*****</a></p>

