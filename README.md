# Lab19-1-2
#include <stdio.h>

int main(void)
{
    char fname[20] = "number.txt";
    FILE *out;
    puts("Создание/добавление в файл");
    
    // Изменяем параметр fopen на "at" (добавление текста)
    if ((out = fopen(fname, "at")) == NULL)
    {
        printf("Ошибка открытия файла для записи");
        return 0;
    }
    
    // Добавляем число 12.56 с новой строки
    fprintf(out, "%.2f\n", 12.56);
    
    fclose(out);
    return 1;
} 1


#include <stdio.h>
#include <math.h>

int main(void)
{
    double start, end, step, x, y;
    int choice;
    FILE *file;

    // Ввод интервала и шага
    printf("Табулирование функции: y = x^2 - 3*cos^2(1.04*x)\n");
    printf("Введите начало интервала (например, 0.15): ");
    scanf("%lf", &start);
    printf("Введите конец интервала (например, 2.1): ");
    scanf("%lf", &end);
    printf("Введите шаг табуляции: ");
    scanf("%lf", &step);

    if (step <= 0)
    {
        printf("Шаг должен быть положительным.\n");
        return 0;
    }

    // Выбор режима записи
    printf("Выберите действие:\n");
    printf("1 - запись в новый файл (очистить файл, если он существует)\n");
    printf("2 - дозапись в существующий файл\n");
    scanf("%d", &choice);

    if (choice == 1)
        file = fopen("temp.txt", "wt");
    else if (choice == 2)
        file = fopen("temp.txt", "at");
    else
    {
        printf("Неверный выбор.\n");
        return 0;
    }

    if (file == NULL)
    {
        printf("Ошибка открытия файла.\n");
        return 0;
    }

    // Заголовок таблицы в файл
    fprintf(file, "x\t\ty\n");
    fprintf(file, "-------------------\n");

    // Табулирование
    for (x = start; x <= end + 1e-9; x += step)
    {
        y = x * x - 3.0 * pow(cos(1.04 * x), 2);
        fprintf(file, "%.4f\t%.4f\n", x, y);
    }

    fclose(file);
#2


    
    printf("Результаты сохранены в temp.txt\n");
    return 0;
}
