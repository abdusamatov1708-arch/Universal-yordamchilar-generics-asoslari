# Universal-yordamchilar-generics-asoslari
TypeScript
// 1. <T> bilan generic funksiya va type inference
function birinchiElement<T>(arr: T[]): T {
    return arr[0];
}

/*
  ------------------------------------------------------------
  TYPE INFERENCE (Turni avtomatik aniqlash) IZOHI:
  ------------------------------------------------------------
  Funksiyani chaqirganda turini qo'lda ko'rsatish shart emas. 
  TypeScript uzatilayotgan massiv turi asosida T o'zgaruvchisi 
  qanday tur ekanligini o'zi avtomatik aniqlaydi.
*/

const sonlarMassivi = [10, 20, 30];
const matnlarMassivi = ["salom", "dunyo"];

const birinchiSon = birinchiElement(sonlarMassivi);   // T avtomatik 'number' bo'ladi
const birinchiMatn = birinchiElement(matnlarMassivi); // T avtomatik 'string' bo'ladi


// 2. Qiymat saqlovchi generic interfeys
interface Quti<T> {
    qiymat: T;
}

const sonQutisi: Quti<number> = { qiymat: 100 };
const matnQutisi: Quti<string> = { qiymat: "Generic Interfeys" };


// 3. extends bilan generic constraint (cheklov) qo'llash
function uzunlikniChopEtish<T extends { length: number }>(item: T): void {
    console.log(`Uzunligi: ${item.length}`); // .length xususiyatiga xavfsiz kirish
}

uzunlikniChopEtish("TypeScript"); // string'da length bor — xato bermaydi
uzunlikniChopEtish([1, 2, 3]);    // massivda length bor — xato bermaydi


/*
  ------------------------------------------------------------
  CONSTRAINT'GA MOS KELMAYDIGAN TUR XATOSI
  ------------------------------------------------------------
  Agar quyidagicha yozishga urinsak:
  `uzunlikniChopEtish(500);`
  
  IZOH: TypeScript kompilyatsiya xatosini beradi. 
  Sababi: 'number' (masalan, 500 soni) .length xususiyatiga ega emas. 
  Generic constraint (`extends { length: number }`) tufayli TypeScript 
  faqat length xususiyati mavjud bo'lgan turlarni qabul qilishni qat'iy talab qiladi.
*/
