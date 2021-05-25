# ipt-jpeg
Bu, gri tonlamalı görüntüler için JPEG sıkıştırma algoritmasının bir uygulamasıdır.

Jupyter not defterinde, kodlama ve kod çözme sürecinde adım adım ilerliyorum. Dizüstü bilgisayar ayrıca Ayrık Kosinüs Dönüşümünün vektörleştirilmiş bir uygulamasını da sunar

Demo: Sıkıştırmadan önceki HD görüntü
![Original_HD_grayscale](https://user-images.githubusercontent.com/65457096/119478855-d26c0b80-bd58-11eb-9e49-6a83a855067f.jpeg)
Orijinal boyutunun 1 / 10'u oranında sıkıştırılmış akış uzunluğuna sahip sıkıştırmadan sonraki görüntü
![Compressed_with_specs](https://user-images.githubusercontent.com/65457096/119478944-dd26a080-bd58-11eb-81c3-9f03744d225a.jpeg)
Yerel makinemde (i7-8550u), sıkıştırma 4 ila 5 saniye sürer. Bu aynı zamanda defterin içinde de rapor edilir.

Endocidng algoritmasının adımları
Bir görüntü üst üste binmeyen 8x8 bloklara bölünmüştür
Her blok için, gerçek bir frekans alanı gösterimi olan ilgili Ayrık Kosinüs Dönüşümünü (DCT) hesaplıyoruz.
Doğal görüntüler düşük frekans bölgesini işgal etme eğilimindedir, bu nedenle DCT matrisi genellikle seyrek bir matristir
DCT katsayı matrisini , görüntünün görsel kalitesini çok fazla etkilemeden bir qunatizasyon tablosu ile elemnetwise bölüp yuvarlayarak daha seyrek hale getirebiliriz . Bu nedenle, niceleme tablosu, kalite ve sıkıştırmanın kapsamı arasında bir değiş tokuş sunar.
Daha sonra her bloğu bir 1D dizisine açacağız. Daha sonra matris seyrekliğinden, önce matrisi bir ZigZag deseninde geçerek, sıfırların sürekli diziler oluşturma eğiliminde olduğu şekilde, kaldırabiliriz. Bu diziler, Runlength kodu kullanılarak sıkıştırılabilir (kayıpsız)
Runlengh kodunun çıktısı, Huffman kodunu kullandığım entropi kodu kullanılarak daha fazla sıkıştırılır (kayıpsız)
Son sıkıştırılmış akışın uzunluğu orijinal akışla karşılaştırılır ve böylece sıkıştırma oranını hesaplayabiliriz
Sıkıştırılmış akışın kodunu çözmek için her adım tersine çevrilir.
