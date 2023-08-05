# ListClass
www.patika.dev
--------------

package listeSınıfı;

import java.lang.reflect.Array;
import java.util.Arrays;

public class BenimListem<T> {
	private Object[] dizi;
    private int boyut;
    private static final int BASLANGIC_BOYUTU = 10;
    
    public BenimListem() {
        this.dizi = new Object[BASLANGIC_BOYUTU];
        this.boyut = 0;
    }
    
    public BenimListem(int kapasite) {
        this.dizi = new Object[kapasite];
        this.boyut = 0;
    }
    
    public int boyut() {
        return boyut;
    }
    
    public int kapasite() {
        return dizi.length;
    }
    
    public void ekle(T veri) {
        if (boyut == dizi.length) {
            kapasiteyiArtir();
        }
        dizi[boyut] = veri;
        boyut++;
    }
    
    public T getir(int indeks) {
        if (indeks < 0 || indeks >= boyut) {
            throw new IndexOutOfBoundsException("Geçersiz indeks: " + indeks);
        }
        return (T) dizi[indeks];
    }
    
    private void kapasiteyiArtir() {
        int yeniKapasite = dizi.length * 2;
        Object[] yeniDizi = new Object[yeniKapasite];
        System.arraycopy(dizi, 0, yeniDizi, 0, boyut);
        dizi = yeniDizi;
    }
    
    public T get(int indeks) {
        if (indeks < 0 || indeks >= boyut) {
            return null;
        }
        return (T) dizi[indeks];
    }
    
    public T remove(int indeks) {
        if (indeks < 0 || indeks >= boyut) {
            return null;
        }

        T silinenVeri = (T) dizi[indeks];

        
        for (int i = indeks; i < boyut - 1; i++) {
            dizi[i] = dizi[i + 1];
        }

        
        dizi[boyut - 1] = null;
        boyut--;

        return silinenVeri;
    }
    
    public T set(int indeks, T veri) {
        if (indeks < 0 || indeks >= boyut) {
            return null;
        }

        T eskiVeri = (T) dizi[indeks];
        dizi[indeks] = veri;
        return eskiVeri;
    }
    
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("[");
        for (int i = 0; i < boyut; i++) {
            sb.append(dizi[i]);
            if (i < boyut - 1) {
                sb.append(", ");
            }
        }
        sb.append("]");
        return sb.toString();
    }
    
    public int indexOf(T veri) {
        for (int i = 0; i < boyut; i++) {
            if (veri.equals(dizi[i])) {
                return i;
            }
        }
        return -1;
    }
    
    public int lastIndexOf(T veri) {
        for (int i = boyut - 1; i >= 0; i--) {
            if (veri.equals(dizi[i])) {
                return i;
            }
        }
        return -1;
    }
    
    public boolean isEmpty() {
        return boyut == 0;
    }
    
    public T[] toArray(String[] strings) {
        T[] array = (T[]) new Object[boyut];
        for (int i = 0; i < boyut; i++) {
            array[i] = (T) dizi[i];
        }
        return array;
    }
    
    public void clear() {
        Arrays.fill(dizi, null);
        boyut = 0;
    }
    
    public BenimListem<T> sublist(int start, int finish) {
        if (start < 0 || finish >= boyut || start > finish) {
            throw new IllegalArgumentException("Geçersiz indeks aralığı: " + start + " - " + finish);
        }

        BenimListem<T> altListe = new BenimListem<>(finish - start + 1);
        for (int i = start; i <= finish; i++) {
            altListe.ekle((T) dizi[i]);
        }

        return altListe;
    }
    
    public boolean contains(T veri) {
        return indexOf(veri) != -1;
    }
    
    
}



package listeSınıfı;

import java.util.Arrays;

public class Main {

	public static void main(String[] args) {
        BenimListem<String> stringListem = new BenimListem<>();

        // Eleman ekleme
        stringListem.ekle("Elma");
        stringListem.ekle("Armut");
        stringListem.ekle("Muz");
        stringListem.ekle("Çilek");

        // Liste içeriği
        System.out.println("String Listesi:");
        System.out.println(stringListem);
        
        
        

        // İndeks 1'deki değeri getirme
        int indeks = 1;
        System.out.println("\nIndeks " + indeks + " : " + stringListem.get(indeks));

        // İndeks 2'deki değeri silme
        int silinecekIndeks = 2;
        String silinenEleman = stringListem.remove(silinecekIndeks);
        System.out.println("\nIndeks " + silinecekIndeks + " silindi. Silinen Eleman: " + silinenEleman);
        System.out.println("Güncel Liste:");
        System.out.println(stringListem);

        // İndeks 0'daki değeri değiştirme
        int degistirilecekIndeks = 0;
        String yeniDeger = "Portakal";
        String eskiDeger = stringListem.set(degistirilecekIndeks, yeniDeger);
        System.out.println("\nIndeks " + degistirilecekIndeks + " değiştirildi. Eski Değer: " + eskiDeger + ", Yeni Değer: " + yeniDeger);
        System.out.println("Güncel Liste:");
        System.out.println(stringListem);

        // "Elma" değerinin son indeksini bulma
        String arananDeger = "Elma";
        System.out.println("\nSon indeks of " + arananDeger + " : " + stringListem.lastIndexOf(arananDeger));

        // Liste boş mu?
        System.out.println("\nListe boş mu? " + stringListem.isEmpty());

        // Listeyi diziye çevirme
        
        String[] stringArray = stringListem.toArray(new String[0]);
        System.out.println("toArray: " + Arrays.toString(stringArray));

        // Listeyi temizleme
        stringListem.clear();
        System.out.println("\nListe boş mu? " + stringListem.isEmpty());
    }
}






