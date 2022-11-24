# Trabalho de Programacao
Este trabalho foi proposto na disciplina de Introdução a Computação e tem como objetivo a resolução de um problema (pensado pelo aluno) em linguagens diferentes.


| Aluno | Bernardo Cavanellas Biondini |
| --- | --- |

Uma plataforma precisa informar para os usuários a probabilidade de se ganhar um sorteio. As regras são as seguintes:

- Quanto mais minutos assistidos, mais chance de ganhar. Dessa forma, se um usuário assistiu 20min e um outro 10min, o primeiro tem o dobro de chances de ganhar
- Caso o usuário seja assinante, ele tem o dobro de chances de ganhar, ou seja, seu tempo de tela é dobrado.

A resolução poderá ser da seguinte forma, a depender da linguagem:

- O programa recebe dois arrays, o primeiro array determina se o usuário é ou não assinante, e o segundo determina os minutos assistidos por cada usuário
Para **C**.
- O programa recebe um array de objetos com três campos, o primeiro campo determina se o usuário é ou não assinante, o segundo determina os minutos assistidos por cada usuário e o terceiro é a probabilidade de ganhar.
Para **Java, C#, C++ e Python**

### C

[main.c - IC-C - Replit](https://replit.com/@BernardoCavanel/IC-C#main.c)

```c
#include <stdio.h>
#include <stdlib.h>

void probabilidadeFunc( int *minutos, short *assinantes, int tam ){
  double probabilidades[100];

  int soma = 0;
  
  for(int i = 0; i < tam; i++) {
    printf("i = %d\n", i);
    if(assinantes[i] > 0) minutos[i] = minutos[i] * 2;

    soma += minutos[i];
  }

  for(int i = 0; i < tam; i++) {
    double prob = (((double)minutos[i] / soma) * 100.0);
    probabilidades[i] = prob;
    printf("O usuário %d tem %lf de probabilidade de ganhar\n", i, probabilidades[i]);
  }

}

int main(void) {

  short condition = 1;
  int cont = 0;

  int minutos[100];
  short assinantes[100];

  while(condition) {
    int tempo;
    short isAssinante;
    
    printf("Digite os minutos assistidos:\n");
    scanf("%d", &tempo);
    printf("Digite 1 se for assinante, se não, digite 0:\n");
    scanf("%hd", &isAssinante);

    minutos[cont] = tempo;
    assinantes[cont++] = isAssinante;

    printf("Digite 1 para continuar a leitura ou 0 para parar:\n");
    scanf("%hd", &condition);
  }

  probabilidadeFunc(minutos, assinantes, cont);
  
  return 0;
}
```

### C++

[main.cpp - IC-Cpp - Replit](https://replit.com/@BernardoCavanel/IC-Cpp#main.cpp)

```cpp
#include <iostream>
#include <vector>
using namespace std;

class User {
  bool assinante;
  int minutos;
  double probabilidade;

  public:
    User(int minutos_, bool assinante_) {
      assinante = assinante_;
      minutos = minutos_;
    }
  
    int getMinutos() {
      return minutos;
    }
  
    double getProbabilidade() {
      return probabilidade;
    }
  
    bool getAssinante() {
      return assinante;
    }
  
    void setProbabilidade(double probabilidade_){
      probabilidade = probabilidade_;
    }
  
    void setMinutos(int minutos_){
      minutos = minutos_;
    }
};

int main() {

  vector<User*> usuarios;

  bool condition = true;

  while(condition) {
    int minutos;
    bool isAssinante;
    
    cout << "Digite os minutos assistidos: " << endl;
    cin >> minutos;
    cout << "Digite 1 se for assinante, se não, digite 0:" << endl;
    cin >> isAssinante;

    usuarios.push_back(new User(minutos, isAssinante));

    cout << "Digite 1 para continuar a leitura ou 0 para parar:" << endl;
    cin >> condition;
  }

  int soma = 0;

  for(auto &usuario : usuarios) {
    if( usuario->getAssinante() )  usuario->setMinutos( usuario->getMinutos() * 2 );

    soma += usuario->getMinutos();
  }

  for(auto &usuario : usuarios) {
    double prob = ((usuario->getMinutos() / (double)soma) * 100.0);
    usuario->setProbabilidade( prob );
  }

  for(int i = 0; i < usuarios.size() ; i++ ) {
      cout << "O usuário " <<  i << " tem " << usuarios[i]->getProbabilidade() << "% de ganhar" << endl;
    }
  
}
```

### C#

[main.cs - IC-csharp - Replit](https://replit.com/@BernardoCavanel/IC-csharp#main.cs)

```csharp
using System;
using System.Collections.Generic;

class Program {
  public static void Main (string[] args) {
    bool condition = true;

    List<User> usuarios = new List<User>();

    while( condition ) {
      Console.WriteLine("Digite os minutos assistidos:");
      int tempo = Convert.ToInt32(Console.ReadLine());
      Console.WriteLine("Digite 1 se for assinante, se não, digite 0:");
      bool isAssinante = Convert.ToBoolean(  Convert.ToInt32(Console.ReadLine())  );

      usuarios.Add(new User(tempo, isAssinante));

      Console.WriteLine("Digite 1 para continuar a leitura ou 0 para parar: ");
      int num = Convert.ToInt32( Console.ReadLine() );
      condition = num >= 1 ? true : false;

    }

    int soma = 0;

    foreach(User usuario in usuarios) {

      if(usuario.getAssinante()) usuario.setMinutos(usuario.getMinutos() * 2);

      soma += usuario.getMinutos();
      
    }

    foreach(User usuario in usuarios) {
      
      double prob = ((usuario.getMinutos() / (double)soma) * 100.0);
      usuario.setProbabilidade( prob );
    }

    for(int i = 0; i < usuarios.Count; i++ ) {
      Console.WriteLine( "O usuário " + i + " tem " + usuarios[i].getProbabilidade() + "% de ganhar"  );
    }
    
  }
}

class User {
  bool assinante;
  int minutos;
  double probabilidade;

  public User(int minutos_, bool assinante_) {
    assinante = assinante_;
    minutos = minutos_;
  }

  public int getMinutos() {
    return minutos;
  }

  public double getProbabilidade() {
    return probabilidade;
  }

  public bool getAssinante() {
    return assinante;
  }

  public void setProbabilidade(double probabilidade_){
    probabilidade = probabilidade_;
  }

  public void setMinutos(int minutos_){
    minutos = minutos_;
  }

}
```

### Java

[Main.java - IC-Java - Replit](https://replit.com/@BernardoCavanel/IC-Java#Main.java)

```java
import java.util.ArrayList; 
import java.util.Scanner;

class Main {
  public static void main(String[] args) {
    ArrayList<User> usuarios = new ArrayList<User>();

    boolean condition = true;

    while(condition) {
      Scanner input = new Scanner(System.in);
      
      System.out.println("Digite os minutos assistidos: ");
      int minutos = input.nextInt();
      
      System.out.println("Digite 1 se for assinante, se não, digite 0:");
      boolean isAssinante = input.nextInt() > 0 ? true : false;

      usuarios.add(new User(minutos, isAssinante));

      System.out.println("Digite 1 para continuar a leitura ou 0 para parar:");
      condition = input.nextInt() > 0 ? true : false;
    }

    int soma = 0;

    for(User usuario : usuarios) {
      if( usuario.getAssinante() )  usuario.setMinutos( (usuario.getMinutos() * 2) );

      soma += usuario.getMinutos();
    }

    for(User usuario : usuarios) {
      double prob = ((usuario.getMinutos() / (double)soma) * 100.0);
      usuario.setProbabilidade( prob );
    }

    for(int i = 0; i < usuarios.size() ; i++ ) {
      System.out.println("O usuário " + i + " tem " + usuarios.get(i).getProbabilidade() + "% de ganhar");
    }
    

    
  }
}

class User {
  boolean assinante;
  int minutos;
  double probabilidade;

  public User(int minutos_, boolean assinante_) {
    assinante = assinante_;
    minutos = minutos_;
  }

  public int getMinutos() {
    return minutos;
  }

  public double getProbabilidade() {
    return probabilidade;
  }

  public boolean getAssinante() {
    return assinante;
  }

  public void setProbabilidade(double probabilidade_){
    probabilidade = probabilidade_;
  }

  public void setMinutos(int minutos_){
    minutos = minutos_;
  }

}
```

### Python

[main.py - IC-py - Replit](https://replit.com/@BernardoCavanel/IC-py#main.py)

```python
class User():
  def __init__(self, minutos, assinante, probabilidade):
        self.minutos = minutos
        self.assinante = assinante
        self.probabilidade = probabilidade

def probabilidade(usuarios):
  soma = 0
  for usuario in usuarios:
    if usuario.assinante == True:
      usuario.minutos *= 2
    soma += usuario.minutos

  for usuario in usuarios:
    usuario.probabilidade = ( usuario.minutos/soma*100 )

condition = True
usuarios = []

while condition:
  tempo = int(input("Digite o numero de minutos assistidos: "))
  isAssinante = bool(int(input("Digite 1 se for assinante, se não, digite 0: ")))

  user = User(tempo, isAssinante, 0)
  
  usuarios.append( user )

  condition = int(input("Digite 1 para continuar a leitura ou 0 para parar: "))

probabilidade(usuarios)

for i, usuario in enumerate(usuarios):
    print("O usuario "+ str(i) + " tem " + str(usuario.probabilidade) + "% de ganhar")
```
