#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>
#include <windows.h>
using namespace std;

int main()
{
  SetConsoleCP(1251);
  SetConsoleOutputCP(1251);
  ifstream inputFile("graph.txt");
  int n, m;
  inputFile >> n >> m;
  int** array;
  array = new int* [m];
  for (int i = 0; i < m; i++) {
    array[i] = new int[1];
  }
  for (int i = 0; i < m; i++) {
    inputFile >> array[i][0] >> array[i][1];
  }
  inputFile.close();

  cout << "З файлу було зчитано такі значення: " << endl;
  for (int i = 0; i < m; i++) {
    cout << array[i][0] <<" "<< array[i][1] << endl;
  }

  //Матриця інцидентності буде розмірності n x m
  int p, t;
  int** incid = new int* [n + 1];
  for (int i = 0; i < n + 1; i++) {
    incid[i] = new int[m + 1];
  }
  for (int i = 0; i < n+1; i++) {
    for (int j = 0; j < m+1; j++) {
      incid[i][j] = 0;
    }
  }
  for (int i = 0; i < n + 1; i++) {
    for (int j = 0; j < m + 1; j++) {
      incid[i][0] = i;
      incid[0][j] = j;
    }
  }
  for (int i = 0; i < m; i++) {
    p = array[i][0];
    t = array[i][1];
    if (p == t)
      incid[p][i + 1] = 2;
    else if (p != t) {
      incid[t][i + 1] = 1;
      incid[p][i + 1] = -1;
    }
  }

char choice;
  cout << "Вивести таблицю інцидентності? (оберіть y/n) ";
  cin >> choice;
  if (choice == 'y') {
    for (int i = 0; i < n + 1; i++) {
      for (int j = 0; j < m + 1; j++) {
        cout << setw(4) << incid[i][j] << " ";
      }
      cout << endl;
    }
  }

  //------Матриця суміжності---------//
  int** symiznist = new int* [n + 1]; //розмір матриці - n x n
  for(int i = 0; i < n + 1; i++) {
    symiznist[i] = new int[n + 1];
  }
  for (int i = 0; i < n + 1; i++) {
    for (int j = 0; j < n + 1; j++) {
      symiznist[i][j] = 0;
    }
  }
  for (int i = 0; i < n + 1; i++) {
    for (int j = 0; j < n + 1; j++) {
      symiznist[i][0] = i;
      symiznist[0][j] = j;
    }
  }
  for (int i = 0; i < m; i++) {
    p = array[i][0];
    t = array[i][1];
    symiznist[p][t] = 1;
  }

  cout << endl << "Вивести таблицю суміжності? (оберіть y/n) ";
  cin >> choice;
  if (choice == 'y') {
    for (int i = 0; i < n + 1; i++) {
      for (int j = 0; j < n + 1; j++) {
        cout << setw(4) << symiznist[i][j] << " ";
      }
      cout << endl;
    }
  }

  system("pause>0");
}
