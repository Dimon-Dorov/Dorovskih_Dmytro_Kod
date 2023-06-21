# Dorovskih_Dmytro_Kod
Курсова робота по темі: гра "Карта скарбів"
#include <stdio.h> //для роботи з файлами

struct Point 
{ //Створення структури для збереження координат
    int x, y;
};

Point find() 
{
    Point tr = {0, 0};  //змінна в якій зберігаються координати (з початковими координатами)
    FILE* inputFile = fopen("input.txt", "r"); //відкриття файлів
    FILE* outputFile = fopen("output.txt", "w");
    int n;
    fscanf(inputFile, "%d", &n); //зчитування кількості вказівок
    if (n < 1 || n > 40) 
	{ // перевірка правильної кількості вказівок
        fprintf(outputFile, "Invalid number of pointers!\n");
        return tr;
    }
    int ins[n][2]; //створення двовимірного масиву, в якому зберігаєються вказівки
    for (int i = 0; i < n; i++) 
	{
        fscanf(inputFile, "%d %d", &ins[i][0], &ins[i][1]);
        if (ins[i][1] < 1 || ins[i][1] > 1000) 
		{ //перевірка правильної кількості кроків
            fprintf(outputFile, "Invalid number of steps!\n");
            return tr;
        }
    }

    for (int i = 0; i < n; i++) 
	{ //цикл для визначення координат
        int a = ins[i][0];
        int steps = ins[i][1];
        switch (a) 
		{
            case 1: // північ
                tr.y += steps;
                break;
            case 2: // північний схід
                tr.x += steps;
                tr.y += steps;
                break;
            case 3: // схід
                tr.x += steps;
                break;
            case 4: // південний схід
                tr.x += steps;
                tr.y -= steps;
                break;
            case 5: // південь
                tr.y -= steps;
                break;
            case 6: // південний захід
                tr.x -= steps;
                tr.y -= steps;
                break;
            case 7: // захід
                tr.x -= steps;
                break;
            case 8: // північний захід
                tr.x -= steps;
                tr.y += steps;
                break;
            default:// невідомий напрямок
                fprintf(outputFile, "Invalid direction!\n");
            return tr;
        }
    }
    fclose(inputFile); //Закриваємо файли
    fclose(outputFile);
	return tr;
}

int main() 
{
    FILE* inputFile = fopen("input.txt", "r"); //відкриття файлів
    FILE* outputFile = fopen("output.txt", "w");
    Point tr = find(); //Отримання координат з функції
    fprintf(outputFile, "%d %d", tr.x, tr.y); //Виведення координат
    fclose(inputFile); //Закриваємо файли
    fclose(outputFile);
    return 0;
}
