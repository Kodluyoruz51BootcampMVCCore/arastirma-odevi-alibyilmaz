---


---

<h1 id="azure-devops-ile-uygulama-derleme-ve-dağıtma">Azure DevOps ile Uygulama Derleme ve Dağıtma</h1>
<p>Mehmet Kut</p>
<h3 id="devops-nedir">DevOps nedir?</h3>
<p>"Devops is the union of the people, process ve products to enable continuous delivery of value to business and it end-users…/ insan, süreç ve ürünlerin sürekli şekilde son kullanıcıya bir değer üretmesine Devops denir" Donovan Brown, Microsoft</p>
<p>The cycle of build-develop-deploy</p>
<h3 id="introducing-azure-devops">Introducing Azure DevOps</h3>
<p><img src="http://image.prntscr.com/image/fwlgJPt1RE_78AAhHbKOZw.png" alt="s1"></p>
<h4 id="azure-devops-tool-kitleri">Azure DevOps Tool kitleri</h4>
<p>Azure Boards – agile tools to plan,track and discuss</p>
<p>Azure Pipelines – build, test and deploy with CI/CD that works with any lang. Platform and cloud. Connect to github or etc.</p>
<p>Azure Repos – cloud - hosted private git repos and collobrate to build better code with pull requests</p>
<p>Azure Test Plans – test and ship</p>
<p>Azure Artifacts – create, host, and share packages w/ your team, add artifacts to your CI/CD pipelines w/ a single click</p>
<h3 id="benefits">Benefits</h3>
<p>Quick set/up</p>
<p>Maintenance-free operations</p>
<p>Easy collobration across domains</p>
<p>Elastic scale</p>
<p>Rock-solid security</p>
<p>Access to cloud-running</p>
<h3 id="azure-pipeline">Azure Pipeline</h3>
<p>Host any lang, platform, any cloud</p>
<p>The deployment not for only azure cloud, enable for in addition to azure, AWS,GCP and on-prem</p>
<p>Building a pipeline for .net core app</p>
<p>1.New build pipeline</p>
<ol start="2">
<li>
<p>Select source control env.</p>
</li>
<li>
<p>Select repo</p>
</li>
<li>
<p>Azure pipelines analyzes the src code and prvd "options" for build</p>
</li>
<li>
<p>This results in a "Azure-pipelines.yml" file</p>
</li>
<li>
<p>Create and Run your Build</p>
</li>
</ol>
<h3 id="demo">Demo</h3>
<p>Yukarıdaki adımlar izlenerek Azure pipeline'da pipeline create ediliyor. Ardından VS üzerinde basic bir <a href="http://ASP.Net">ASP.Net</a> Core uygulaması açıldı Git'e dahil edilerek Azure'da publish seçeneğine tıklanıyor, ardında repo seçilerek repo publish ediliyor. Bu şekilde oluşturulan repo Azure Pipeline üzerine geçiriliyor.</p>
<p>Azure pipeline ASP .Net Core olarak configure ediliyor ve commit ediliyor. Ardından build aşamalarından geçiyor ve pipeline oluşması sonucu bir artifact dosyası yaratılıyor.</p>
<h3 id="deploy-süreci">Deploy süreci</h3>
<p>Azure Pipeline Release özelliği ile deployment yapılabiliyor. Bu aşamada release özelliği tıklanarak stage aşamaları hangisi tercih ediliyorsa oluşturuluyor(prod,staging,test etc.), deploy edilecek stage Azure Web App seçilerek Linux ortamda .Net Core runtime'a sahip bir stage'de release edilebiliyor.</p>
<p>Bu aşamada Create new Pipeline denerek, Azure Web App seçiliyor, az önce repo edilen demo artifact ve production içerisinde Azure subscribation seçilerek, App Type Web App on Linux seçiliyor. Save edilerek Pipeline tasarlanmış oluyor.</p>
<p>Save ettikten sonra ise Create Release butonu oluşuyor. Bu buton tıklandıktan sonra mevcut artifact seçiliyor ve release oluşuyor ve auto deployment seçiliyken production pipeline üzerinde deployment başlatılıyor ve <a href="http://portal.azure.com">portal.azure.com</a>'da deployment başarılı bir şekilde sonlanarak demo canlıya çıkıyor.</p>
<p>Örneğin 3 servisi olan(staging,test, prod) bir uygulamada 100 deployment yapılmak istendiğinde monolitik yöntemle 300 deployment yapılması gerekir. Ancak Azure Pipeline ve release ile çok daha sürdürülebilir bir CI/CD süreci mümkün hale geliyor.</p>
<p>Open Source projeler için Azure Pipeline'da sınırsız build minutes mevcut. Bunun dışında 1 agent değil 10 ücretsiz paralel Windows, Linux ve macOS veriliyor.</p>
<h2 id="agents">Agents</h2>
<h3 id="microsoft-hosted-agents">Microsoft-Hosted Agents</h3>
<p>Microsoft'un daha önce kullanım için hazırladığı sanal linkinler olarak tanımlamak mümkün. Bunlara erişiminiz olmuyor ancak uygulamanız örneğin Ubuntu veya VS gerektiriyorsa bunu seçebiliyorsunuz.</p>
<p><a href="https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/hosted?view=azure-devops&amp;tabs=yaml">https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/hosted?view=azure-devops&amp;tabs=yaml</a></p>
<p>Bu link üzerinden hangi ortamlar ve arkaplanda derleme yapılması için hangi toolların kullanıldığı ile ilgili detaylar mevcut. Chocolatey ile mevcutta bulunmayan toollar da kurulabilir. Ancak bu kurulum örn. 2dk sürmekteyse pipeline her açıldığında o süre kadar bekler. Build çıktısı olarak max. 10 GB bir çıktı limiti mevcut. Build agentlar en fazla 6 saat çalışabiliyor ve Windows administrator ve şifresiz Linux sudo userı kullanıcısı supervisor olarak çalışıyor. Windows makinaya RDP veya başka bir yöntemle login olunamıyor.</p>
<h3 id="self-hosted-agents">Self-Hosted Agents</h3>
<p>Bu agent formatında siz kendi makinalarınızı build veya release agenta çeviriyorsunuz, bu sayede esnek olarak derlemeyi kendi ortamlarınızda yapabiliyorsunuz. Olmayan toolları her defasında yeniden kurmak durumunda kalmıyorsunuz.</p>
<p><img src="http://image.prntscr.com/image/q8bpJU5fTjeg9daiM67rHA.png" alt="s2"></p>
<h3 id="microsoft-hosted-agents-vs.-self-hosted-agents">Microsoft-Hosted Agents vs. Self-Hosted Agents</h3>
<p>Microsoft Hosted-Agents bakım gerektirmiyor buna karşın Self-Hosted Agents bakım gerektiriyor. MS host-agents ayda 1 otomatik olarak güncelleniyor.</p>
<p>MS host agents firewall arkasında çalışmıyor(çalışabiliecek şekilde kurgulanabilir) ancak Self hosted agents çalışabiliyor.</p>
<p>MS host agents self hosted agentsa göre derleme ve artifact çıkma hızında cachinglerinden dolayı daha yavaş kalabiliyor.</p>
<p>MS host agentta çıktığınız releasein süresi yoğunluğa bağlı artabiliyor, selfte size ait olduğunda eğer çalışıyorsa direk başlıyor.</p>
<h3 id="demo-2">Demo 2</h3>
<p><a href="http://image.prntscr.com/image/7mR2TyfmRV_zPb3dfiKV4A.png">http://image.prntscr.com/image/7mR2TyfmRV_zPb3dfiKV4A.png</a></p>
<p>Azure repos'a bir <a href="http://ASP.NET">ASP.NET</a> uygulaması gönderilerek, bu repoyu MS-Hosted Agentta derleyip, çıktı artifact bir ISS makinası Self-Hosted olarak kurgulanarak uygulama ISS üzerine deploy ediliyor.</p>
<p>MVC bir ASP .Net uygulaması oluşturuldu. Bunun pipeline'ı hazırlandı. Bu MVC <a href="http://ASP.NET">ASP.NET</a> uygulamasından artifact çıkarılarak release self hosted Agent deployment grouptan Azure'a register ediliyor ve makine üzerine deploy ediliyor.</p>
<h1 id="serverless-ai">Serverless AI</h1>
<p>Daron Yöndem</p>
<p>AI ile ilgili yaygın yaklaşım esasen General AI'ın insansı düşünen bir AI olduğudur ancak akademik dünya'da böyle olduğuna dair bir ortaklaşma bulunmamakta olup, gelişen pratikler bundan uzaktadır.</p>
<p>AI ile ilgili yine yaygın sunumlarda AI biliminin dallarını belirten bir slayt gösterilir. Bunu gösterilen dalların tümüne vakıf olunabileceği hayalini yaratır ancak bu düşünce rasyonel değildir. Belirli bir alan seçip oraya yoğunlaşmak gerekmektedir, aksi durum hiçbir çıktı almaksızın verimsiz enerji harcanmasına neden olabilir.</p>
<p>Serverless AI'da da C ve C++ plus dillerinin günümüzde daha product odaklı C#, Java vb. dillere evrilmesine benzer bir dönüşüm mevcuttur. Şirketlerin AI bilimini uygulayabilecek matemetik bilgisine sahip personel bulundurma olanağı bulunmadığından eskiden kendi insan kaynağını belirli anlaşmalar karşılığı kullandıran büyük yazılım şirketleri, bugün ilk bahsedilen örnekteki gibi, yaygınlaşması ve kullanılabilirliği için kolaylaştırmalar sağlamışlardır. Microsoft'da bu şirketlerden biridir.</p>
<p>Microsoft geçmiş alışkanlıklarının aksine AI alanına girerken aşağıdan yukarı bir yöntemle başlamayı denemiştir. Serverless AI ise basitçe, AI yapılması istenip altyapısı yani serverlarla uğraşmak istenmemesine yönelik olmasıdır. Bunun bazı avantajları ise hiçbir şeyin maintain etmenize scan etmenize gereksinim duyulmaması ile birlikte kullanılan kadar ödeme bütçesi oluşturması olarak sıralanabilir. Bu avantajlarla birlikte serverda AI kullanılması için gerekli component ve toollarla da vakit kaybedilmeyip, serverless AI'larda süreç rest APIler üzerinden ilerlemektedir. Bütün bunlar ise çok hızlı bir şekilde pazara çıkılabilmesini sağlamaktadır.</p>
<p>QnA maker: Web sitenizde bir SSS varsa ve data science ile ilgilenebilecek bir şirket değilseniz, bu uygulamayı kolayca kurup sayfanın linkini girdiğinizde size bir chatbot sağlıyor ve bu chati iframe tagiyle sayfaya yerleştirebiliyorsunuz. Data science ilgili birçok süreç içerisinden uçtan uça bir çözüm sunulmuş oluyor. Customize etmek için Azure Portal'a gittiğinizde chatbot'un C# çıktısını size sunuyor ve burdan flow'ları dilediğiniz özelleştirmeyi yapabiliyorsunuz.</p>
<p>Serverless AI ile kullanılabilecek bazı yardımcı araçlar:</p>
<p><img src="http://image.prntscr.com/image/PLY2cTUxS1GuU8duYPYATg.png" alt="s4"></p>
<h3 id="face-recognition">Face recognition</h3>
<p>Face detection – resim içindeki yüzleri algılama, yüzdeki burun göz vs konumlarını algılama</p>
<p>Face verification/grouping - unique person üretme ve grup içerisinde tanıma</p>
<p>Similar face searching - kişiye benzer fotoğraf arama</p>
<p>Face identification - kişiye ait fotoğraf arama</p>
<h3 id="demo-1">Demo</h3>
<p><img src="http://image.prntscr.com/image/sH4di8lwTouAr95TEhDX7Q.png" alt="s5"></p>
<p>Visual Studio üzerinden basit kodlarla ve Azure üzerinden expose edilen API'ler ile face detection demosu yapılıyor. Kısaca anlatmak gerekirse, FaceLandmark parametresi ile yüzün göz kısmında bir dikdörtgen oluşturuluyor ve o bölge blurlanıyor.</p>
<h3 id="computer-vision">Computer Vision</h3>
<p>Burada bir resim üzerinde bu resimde ne varsa analiz edilebiliyor. Objeler bulunabiliyor, metin varsa tanıyor ve output ediyor, OCR(optical character recognition) yapabiliyor, meşhur insanları tanıyabiliyor. Bir başka özellik, Generate Thumbnail API(smart thumbnail), kullanımına örnek olarak; Twitter'da herhangi bir fotoğraf tweetlerseniz timeline'a geçtiğinizde o fotoğraf croplanıyor. Bu croplamaya dikkat edilirse akıllı bir croplama yapılıyor, point of interest denilen alanı yakalayarak onu ekranda tutabiliyor.</p>
<h3 id="demo-3">Demo</h3>
<p><img src="http://image.prntscr.com/image/eqqWOKx1Rre1iCAULsNNjA.png" alt="s6"></p>
<p>Bu örnekte GenerateThumbnailAsync çağrılırak image url veriliyor ve 500*500 oranında croplama komutu veriliyor. Yine aynı yöntemle bir endpoint ile image urli birleştirilerek uygulama çalıştırılıyor. Normal biçimde croplansa resimde oturan adamın yarısı kırpılacakken sağ tarafta duran insanın point of interest olduğunu yakalıyor ve sol taraftan daha fazla kesiyor.</p>
<p><img src="http://image.prntscr.com/image/a5OUK3gXRuu0xSs4PqOoNw.png" alt="s7"></p>
<h3 id="video-indexer">Video Indexer</h3>
<p>Video Indexer, videoya oto altyazı sağlayabiliyor, insight verebiliyor videodaki yüzleri yakalayabiliyor, unique konuşan insanları algılayabiliyor. Hangi dakikalarda aynı insanın nasıl bir duyguyla konuştuğunu anlayabiliyor ve translate yapabiliyor. 18 farklı API üzerinde çalışılabiliyor. (Hoca uzun sürebileceği için demo tercih etmiyor)</p>
<h3 id="custom-vision">Custom Vision</h3>
<p>Daha önceki servislerde bir fotoğraftaki basit objeler tanınabiliyordu ama her obje tanınmayabilir. Bu serviste halihazırda tanımlı olmayan modelleri train ederek kendiniz tanıtarak rest API ile kullanabiliyorsunuz. Daha fazla AI ile ilişkili bir uygulama olmasına rağmen aynı basitlikte kullanılabiliniyor.</p>
<h3 id="demo-4">Demo</h3>
<p><img src="RackMultipart20200605-4-17pf8x1_html_73a8a29059473acc.png" alt=""></p>
<p>Bu demo, localde bulunan herhangi bir fotoğraf train edilerek evaluate edilip API olarak başka bir uygulama için dışarı çıkabiliyor. Öncelikle Azure Portal üzerinde customvisionservice servisi(ücretsiz) ile quick startla başlanıyor ve <a href="http://customvision.ai">customvision.ai</a> adresine bağlanılıyor.</p>
<p>Sign in - New project – isim verme – classification – multiclass (single tag per a image) - Domain:General (compact domain seçilirse export yapılabiliyor) seçenekleri ile proje oluşturuluyor.</p>
<p>Resimler yükleniyor (araba resimi - 30 adet) upload ediliyor.</p>
<p>5 adet otobüs resmi upload ediliyor.</p>
<p>Train butonuna basılarak train işlemi başlatılıyor. İşlem bittikten sonra qucik test ile resim yüklenip test ediliyor ve size yüzde kaç araba veya otobüs olduğunun çıktısını veriyor.</p>
<h3 id="speech">Speech</h3>
<p>Speech to text – text to speech, speech recognition, speech translation gibi hizmetler real time olarak dahi yapılabiliyor.</p>
<h3 id="demo-5">Demo</h3>
<p>Bu demoda ssmlXMLTemplate ile Türkçe fontu tanıtılıyor, tokenla authtoken olunuyor ve sgml XML Template ile sonunda texttoRead nesnesi ile text okunarak mpg formatına çevriliyor. Uygulama çalıştırıp tarayıcıda endpoint sonuna "?text=Merhaba" yazıldığında bir mp3 dosyası iniyor ve açıldığında merhaba sesi duyuluyor.</p>
<h3 id="language">Language</h3>
<p>Dil kısmında sentiment analysis çok popüler, text verip onun duygusunu yakalama için kullanılıyor. Translation. Content Moderator, küfür ve pornografiyi tanıyabiliyor ve bir insan oturuyor gibi ekran çıkartarak bu iyi bu kötü diyebiliyor. Bing spell checking, Türkçe 'de eksik ama yurtdışı için kullanılabiliyor.</p>
<h3 id="demo-6">Demo</h3>
<p>Bu demoda kodda bulunan 'hava güzel' 0 olumlu, 'hava rezalet' 1 olumsuz ve 'hava nasıl?' 2 nötr olarak tanınması isteniyor. TextAnalyticsClient oluşturularak sentimentAsync içerisine bu textler yazılıyor ve yine endpoint olarak çalıştırıldığında çıktısında 0, 1 ve 2'nin duygusunu tanıyarak % verek oranlıyor. Bu oranlar ne kadar pozitif olduğunu açıklıyor, negatifi ise daha düşük bir pozitif olma oranıyla açıklıyor.</p>

