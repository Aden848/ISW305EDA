
/******************************************************************************

Welcome to GDB Online.
GDB online is an online compiler and debugger tool for C, C++, Python, Java, PHP, Ruby, Perl,
C#, OCaml, VB, Swift, Pascal, Fortran, Haskell, Objective-C, Assembly, HTML, CSS, JS, SQLite, Prolog.
Code, Compile, Run and Debug online from anywhere in world.

*******************************************************************************/
#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Libro {
private:
    string titulo;
    string autor;
    int anio;

public:
    Libro(string t, string a, int an)
        : titulo(t), autor(a), anio(an) {}

    string getTitulo() {
        return titulo;
    }

    string getAutor() {
        return autor;
    }

    int getAnio() {
        return anio;
    }
};

class Biblioteca {
private:
    vector<Libro> libros;

public:

    void agregarLibro() {
        string titulo, autor;
        int anio;

        cin.ignore();

        cout << "Titulo: ";
        getline(cin, titulo);

        cout << "Autor: ";
        getline(cin, autor);

        cout << "Anio de publicacion: ";
        cin >> anio;

        libros.push_back(Libro(titulo, autor, anio));

        cout << "\nLibro agregado correctamente.\n";
    }

    void ordenarPorAnio() {

        int n = libros.size();

        for (int i = 0; i < n - 1; i++) {

            for (int j = 0; j < n - i - 1; j++) {

                if (libros[j].getAnio() > libros[j + 1].getAnio()) {

                    Libro temp = libros[j];
                    libros[j] = libros[j + 1];
                    libros[j + 1] = temp;
                }
            }
        }

        cout << "\nLibros ordenados correctamente.\n";
    }

    void mostrarLibros() {

        if (libros.empty()) {
            cout << "\nNo hay libros registrados.\n";
            return;
        }

        cout << "\n===== LIBROS REGISTRADOS =====\n";

        for (size_t i = 0; i < libros.size(); i++) {

            cout << "\nTitulo: " << libros[i].getTitulo();
            cout << "\nAutor : " << libros[i].getAutor();
            cout << "\nAnio  : " << libros[i].getAnio();
            cout << "\n-------------------------\n";
        }
    }

    void buscarLibro() {

        if (libros.empty()) {
            cout << "\nNo hay libros registrados.\n";
            return;
        }

        cin.ignore();

        string tituloBuscado;

        cout << "\nIngrese el titulo a buscar: ";
        getline(cin, tituloBuscado);

        bool encontrado = false;

        for (size_t i = 0; i < libros.size(); i++) {

            if (libros[i].getTitulo() == tituloBuscado) {

                cout << "\nLibro encontrado:";
                cout << "\nTitulo: " << libros[i].getTitulo();
                cout << "\nAutor : " << libros[i].getAutor();
                cout << "\nAnio  : " << libros[i].getAnio();

                encontrado = true;
                break;
            }
        }

        if (!encontrado) {
            cout << "\nLibro no encontrado.\n";
        }
    }

    int contarRecursivo(int indice, int anioLimite) {

        if (indice == libros.size())
            return 0;

        if (libros[indice].getAnio() < anioLimite)
            return 1 + contarRecursivo(indice + 1, anioLimite);

        return contarRecursivo(indice + 1, anioLimite);
    }

    void calcularPublicadosAntes() {

        int anio;

        cout << "\nIngrese el anio limite: ";
        cin >> anio;

        int cantidad = contarRecursivo(0, anio);

        cout << "\nCantidad de libros publicados antes de "
             << anio << ": "
             << cantidad << endl;
    }
};

int main() {

    Biblioteca biblioteca;

    int opcion;

    do {

        cout << "\n===================================";
        cout << "\n      SISTEMA BIBLIOTECA";
        cout << "\n===================================";
        cout << "\n1. Agregar libro";
        cout << "\n2. Ordenar por anio";
        cout << "\n3. Buscar libro";
        cout << "\n4. Mostrar libros";
        cout << "\n5. Contar libros antes de un anio";
        cout << "\n6. Salir";
        cout << "\nSeleccione una opcion: ";
        cin >> opcion;

        switch (opcion) {

        case 1:
            biblioteca.agregarLibro();
            break;

        case 2:
            biblioteca.ordenarPorAnio();
            break;

        case 3:
            biblioteca.buscarLibro();
            break;

        case 4:
            biblioteca.mostrarLibros();
            break;

        case 5:
            biblioteca.calcularPublicadosAntes();
            break;

        case 6:
            cout << "\nFin del programa.\n";
            break;

        default:
            cout << "\nOpcion invalida.\n";
        }

    } while (opcion != 6);

    return 0;
}
