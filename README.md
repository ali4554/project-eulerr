Project Euler

PROBLEM 6
Problem ;
 * İlk on doğal sayının karelerinin toplamı,
 * 12 + 22 + ... + 102 = 385
 * İlk on doğal sayının toplamının karesi,
 * (1 + 2 + ... + 10) 2 = 552 = 3025
 * Dolayısıyla, ilk on doğal sayının karelerinin toplamı ile toplamın karesi arasındaki fark 3025 - 385 = 2640'dır.
 * İlk yüz doğal sayının karelerinin toplamı ile toplamın karesi arasındaki farkı bulun.

Çözüm ; 
Bu çözüm, bazı Summation Identities (Türkçesi toplama kimlikleri gibi bisey oluyor) kullanır. (bkz. Http://en.wikipedia.org/wiki/Summation#Identities)
 *Problemi basit bir hesaplamaya dönüştürür.
* Algoritmik Karmaşıklık: O (1)

Kod ;
function topKareFark(n) {
	    return (
	        (3 * Math.pow(n, 4)) +
	        (2 * Math.pow(n, 3)) -
	        (3 * Math.pow(n, 2)) -
	        (2 * n)
	    ) / 12;
	}
	console.log(topKareFark(100));
	


PROBLEM 16
Problem ;
* 2 15 = 32768 ve basamaklarının toplamı 3 + 2 + 7 + 6 + 8 = 26.
* 2 1000 sayısının rakamlarının toplamı nedir ?
Çözüm ;
* İlk önce basamakları bir dizi içine aldım ve kuvvet 0 a inene kadar döngümü yazdım. Basamak sayısını hesaplamak için.
* Daha sonra toplamı hesaplamak için fonksiyonumu yazdım.
*En son  2 cevabıda  console.log a yazdırdım.
Kod ;
var getBasamaklar = function(kuvvet) {
    var basamaklar = [];
    basamaklar[0] = 1;
    while (kuvvet > 0) {
        for (var i = basamaklar.length-1; i >= 0; i--) {
            basamaklar[i] *= 2;
            if (basamaklar[i] > 9) {
                basamaklar[i] -= 10;
                basamaklar[i+1] = basamaklar[i+1] || 0;
                basamaklar[i+1] += 1;
            }
        }
        kuvvet--;
    }

    return basamaklar;
};

var getTop = function(kuvvet){
    var basamaklar = getBasamaklar(kuvvet);
    var top = 0;
    for(var i = basamaklar.length - 1; i >= 0; i--){
        top += basamaklar[i];
    }
    return top;
};

console.log(getTop(15));
console.log(getTop(1000));
PROBLEM 26
Problem ;
* Birim kesir, payda 1 içerir. 2 ila 10 paydaları ile birim fraksiyonların ondalık temsili verilmiştir:
1 / 2	= 	0.5
1 / 3	= 	0 (3)
1 / 4	= 	0.25
1 / 5	= 	0.2
1 / 6	= 	0.1 (6)
1 / 7	= 	0. (142857)
1 / 8	= 	0.125
1 / 9	= 	0 (1)
1 / 10	= 	0.1
* Burada 0.1 (6) 0.166666 ... anlamına gelir ve 1 basamaklı bir tekrarlama döngüsüne sahiptir. 1 / 7'nin 6 basamaklı tekrar eden bir döngüye sahip olduğu görülebilir .
* 1 / d ondalık kesir kısmında en uzun yinelenen döngüyü içeren d <1000 değerini bulun .
Çözüm ;
*İlk yazdığım fonksiyonda 1 den yazdığım değere kadar tüm paydaların hesaplanıp en uzun döngün boyunu ve en uzun sayıyı hesaplayıp sonuç olarak vermesini hesapladım.
*İkinci fonksiyonda da payın önceden tekrarlanıp tekrarlanmadığını, sonraki payı alıp işlemi devam ettirmesiyle ilgili kodlar bulunmakta.
Kod ;
var getEnUzunDongu = function(maxSayi){
    var uzunSayi = 1;
    var uzunDonguBoyu = 1;
    
    for(var guncelSayi = uzunSayi + 1; guncelSayi <= maxSayi; guncelSayi++){
        var donguBoyu = getDonguBoyu(guncelSayi);
        
        if(donguBoyu > uzunDonguBoyu){
            uzunDonguBoyu = donguBoyu;
            uzunSayi = guncelSayi;
        }
    }    
    return uzunSayi ;
};

var getDonguBoyu = function(sayi){
    var payi = 1;
    var paylari = [];
    var paylarBas = [];
    
    while(!basDizisi){
        if(payi == 0){
            return 0;
        }
        
        for(var i = 0; i < paylari.length; i++){
            if(payi == paylari[i]){
                var basDizisi = 0;                
                for(var j = i; j < paylari.length; j++){
                    basDizisi += paylarBas[j];
                }
                
                return basDizisi;
            }
        }         
        paylari[paylari.length] = payi;
        var basamak = 1;
        while(sayi > payi){
            payi *= 10;
            basamak++;
        }
        paylarBas[paylarBas.length] = basamak;           
        paylar = paylar % sayi;
    }
};


console.log(getEnUzunDongu(10));
console.log(getEnUzunDongu(1000));    
PROBLEM 36
Problem ;
* Ondalık sayı, 585 = 1001001001 2 (ikili), her iki bazda palindromiktir.
* Taban 10 ve taban 2'de palindromik olan bir milyondan az olan tüm sayıların toplamını bulun.
(Lütfen her iki tabandaki palindromik sayının baştaki sıfırları içermeyebileceğini unutmayın.)
Kod ;
var isPalindrome = require('is-palindrome');
function toBinary(decimalNumber) {
  return decimalNumber.toString(2);
}
function isPalindromeInBothBases(decimalNumber) {
  return [decimalNumber, toBinary(decimalNumber)].every(isPalindrome);
}
var _ = require('lodash');
console.log(_.sum(_.range(1, 1000000).filter(isPalindromeInBothBases)));
PROBLEM 46
Problem ;
* Christian Goldbach tarafından, her bir tekli kompozit sayının asal ve iki kez bir karenin toplamı olarak yazılabileceği önerildi.
9 = 7 + 2 × 1 2
15 = 7 + 2 × 2 2
21 = 3 + 2 × 3 2
25 = 7 + 2 × 3 2
27 = 19 + 2 × 2 2
33 = 31 + 2 × 1 2
* Bu varsayımın yanlış olduğu ortaya çıktı.
* Bir asal ve iki karenin toplamı olarak yazılamayan en küçük tek kompozit nedir?
Kod ; 
var should = require('should');

function findSquaresLessThanHalf(n) {
  var root = Math.sqrt(n / 2);
  var squaresLessThanN = [];
  var i;
  for (i = Math.floor(root - 0.1); i > 0; i--) {
    squaresLessThanN.unshift(i * i);
  }
  return squaresLessThanN;
}
findSquaresLessThanHalf(9).should.eql([1, 4]);

var isPrime = require('quick-is-prime');

function testConjecture(n) {
  return findSquaresLessThanHalf(n).some(function (square) {
    return isPrime(n - 2 * square);
  });
}
[9, 15, 21, 25, 27, 33].every(testConjecture).should.eql(true);

var i;
for (i = 1; i < 10000; i += 2) {
  if (!isPrime(i)) {
    if (!testConjecture(i)) {
      console.log(i);
    }
  }
}
PROBLEM 56
Problem ;
* Bir googol (10 100 ) çok büyük bir sayıdır: bir tane ardından yüz tane sıfır; 100 100 neredeyse düşünülemeyecek kadar büyük: Biri iki yüz sıfır. Boyutlarına rağmen, her sayıdaki rakamların toplamı sadece 1'dir.
* Formun doğal sayıları göz önüne alındığında, a b , nerede a, b <100, maksimum dijital toplam nedir?
Kod ;
var big = require('big.js')
var _ = require('lodash')
require('should')

function digitalSum(numberString) {
  return _.sum(numberString.toString().split('').map(Number))
}
digitalSum('5231').should.eql(11)

var upperBound = 101
var a, b, sum
var max = {a: 1, b: 1, digitalSum: 1}
for (a = 1; a < upperBound; a++) {
  for (b = 1; b < upperBound; b++) {
    sum = digitalSum(big(a).pow(b).toFixed())
    if (sum > max.digitalSum) {
      console.log(a, b, sum) // 99 95 972
      max = {a: a, b: b, digitalSum: sum}
    }
  }
}



# project-eulerr
