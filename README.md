#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <math.h>

int main() {
    char nama[50];
    char gender;
    double berat, tinggi, bmr, bb_ideal;
    int umur;

    printf("==============================================\n");
    printf("    PROGRAM KALKULATOR BMR & BB IDEAL\n");
    printf("==============================================\n\n");

    // Input data
    printf("Masukkan nama Anda: ");
    fgets(nama, sizeof(nama), stdin);
    

    printf("Masukkan umur (tahun): ");
    scanf("%d", &umur);
    
    printf("Masukkan gender (L/P): ");
    scanf(" %c", &gender);

    printf("Masukkan berat badan (kg): ");
    scanf("%lf", &berat);

    printf("Masukkan tinggi badan (cm): ");
    scanf("%lf", &tinggi);

    // Hitung BMR
    if (toupper(gender) == 'L') {
        bmr = (10 * berat) + (6.25 * tinggi) - (5 * umur) + 5;
    } else {
        bmr = (10 * berat) + (6.25 * tinggi) - (5 * umur) - 161;
    }

    // Hitung Berat Badan Ideal
    if (toupper(gender) == 'L') {
        bb_ideal = (tinggi - 100) - ((tinggi - 100) * 0.1);
    } else {
        bb_ideal = (tinggi - 100) - ((tinggi - 100) * 0.15);
    }

    // Tampilkan hasil
    printf("\n\n==============================================\n");
    printf("           HASIL PERHITUNGAN\n");
    printf("==============================================\n");
    printf("Nama    : %s\n", nama);
    printf("Umur    : %d tahun\n", umur);
    printf("Gender  : %s\n", (toupper(gender) == 'L') ? "Laki-laki" : "Perempuan");
    printf("BMR     : %.2f kkal\n", bmr);
    printf("BB Ideal: %.2f kg\n", bb_ideal);
    printf("==============================================\n");

    // Tentukan status berat badan
    double selisih = fabs(berat - bb_ideal);
    
    printf("\n=== STATUS BERAT BADAN ===\n");
    if (selisih <= 2.0) {
        printf("✅ BERAT BADAN SUDAH IDEAL\n");
        printf(" Berat badan Anda sudah ideal.\n");
    } else {
        printf("❌ BERAT BADAN BELUM IDEAL\n");
        if (berat > bb_ideal) {
            printf("Anda kelebihan berat badan: %.2f kg\n", berat - bb_ideal);
        } else {
            printf("Anda kekurangan berat badan: %.2f kg\n", bb_ideal - berat);
        }
    }

    return 0;
}
