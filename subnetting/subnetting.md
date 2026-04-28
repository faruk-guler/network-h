😷😷 Subnet Mask/Netmask Nedir?
Bir IP adresinin hangi kısmının ağ (network) ve hangi kısmının cihaz (host) adresi olduğunu belirleyen bir parametredir.
Yani, ağ maskesi, bir IP adresinin hangi kısmının ağla, hangi kısmının ise o ağdaki cihazlarla ilişkili olduğunu ayırır.
Daha sonra bunları kullanarak, diğer cihazlarla iletişim kurmanın yolunu bulmaya çalışır.

>>> Subnet Mask neden gerekli?
Neden Subnet'lere ihtiyaç duyarız tek bir ağ yeterli olmaz mı? 
Çok sayıda cihazın bulunduğu devasa ağ hayal edelim, bir bilgisayar diğer cihazlarla iletişim kurması gerektiğinde, ona ulaşmak için bir yayın (broadcast) kullanır.
Ağdaki tüm cihazlara yapılan bu çağrı trafik oluşturarak ağı yavaşlatır.
En büyük nedeni Broadcast trafiğini önlemektir, Bu yüzden ağın küçük alt ağlara bölünmesi gerekir. 
Router kullanılarak ağlar parçalanır ve fiziksel olarak ayrılır. 
Broadcast Router' dan geçemediği için yalnızca bir ağ içerisinde hapsolur ve diğer ağlara erişemez. Bu sayede trafik sorunu ortadan kalkar.
