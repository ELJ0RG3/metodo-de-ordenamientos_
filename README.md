# metodo-de-ordenamientos_
using System;

class Program
{
    static void Main()
    {
        int[] array = { 64, 25, 12, 22, 11 };
        bool salir = false;

        while (!salir)
        {
            Console.WriteLine("\n--- Menú de Ordenamientos ---");
            Console.WriteLine("1. Burbuja");
            Console.WriteLine("2. Sacudida");
            Console.WriteLine("3. Inserción");
            Console.WriteLine("4. Selección");
            Console.WriteLine("5. Shell");
            Console.WriteLine("6. Quicksort");
            Console.WriteLine("7. Heapsort");
            Console.WriteLine("8. Salir");
            Console.Write("Seleccione una opción: ");

            string opcion = Console.ReadLine();
            int[] copia = (int[])array.Clone();

            switch (opcion)
            {
                case "1":
                    Burbuja(copia);
                    break;
                case "2":
                    Sacudida(copia);
                    break;
                case "3":
                    Insercion(copia);
                    break;
                case "4":
                    Seleccion(copia);
                    break;
                case "5":
                    Shell(copia);
                    break;
                case "6":
                    Quicksort(copia, 0, copia.Length - 1);
                    break;
                case "7":
                    Heapsort(copia);
                    break;
                case "8":
                    salir = true;
                    continue;
                default:
                    Console.WriteLine("Opción no válida.");
                    continue;
            }

            Console.WriteLine("Arreglo ordenado: " + string.Join(", ", copia));
        }
    }

    static void Burbuja(int[] arr)
    {
        for (int i = 0; i < arr.Length - 1; i++)
            for (int j = 0; j < arr.Length - i - 1; j++)
                if (arr[j] > arr[j + 1])
                    (arr[j], arr[j + 1]) = (arr[j + 1], arr[j]);
    }

    static void Sacudida(int[] arr)
    {
        int inicio = 0, fin = arr.Length - 1;
        bool intercambio = true;

        while (intercambio)
        {
            intercambio = false;
            for (int i = inicio; i < fin; i++)
            {
                if (arr[i] > arr[i + 1])
                {
                    (arr[i], arr[i + 1]) = (arr[i + 1], arr[i]);
                    intercambio = true;
                }
            }

            if (!intercambio) break;

            intercambio = false;
            fin--;

            for (int i = fin; i > inicio; i--)
            {
                if (arr[i] < arr[i - 1])
                {
                    (arr[i], arr[i - 1]) = (arr[i - 1], arr[i]);
                    intercambio = true;
                }
            }

            inicio++;
        }
    }

    static void Insercion(int[] arr)
    {
        for (int i = 1; i < arr.Length; i++)
        {
            int key = arr[i];
            int j = i - 1;
            while (j >= 0 && arr[j] > key)
            {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = key;
        }
    }

    static void Seleccion(int[] arr)
    {
        for (int i = 0; i < arr.Length - 1; i++)
        {
            int minIdx = i;
            for (int j = i + 1; j < arr.Length; j++)
                if (arr[j] < arr[minIdx])
                    minIdx = j;
            (arr[i], arr[minIdx]) = (arr[minIdx], arr[i]);
        }
    }

    static void Shell(int[] arr)
    {
        int n = arr.Length;
        for (int gap = n / 2; gap > 0; gap /= 2)
        {
            for (int i = gap; i < n; i++)
            {
                int temp = arr[i];
                int j;
                for (j = i; j >= gap && arr[j - gap] > temp; j -= gap)
                    arr[j] = arr[j - gap];
                arr[j] = temp;
            }
        }
    }

    static void Quicksort(int[] arr, int low, int high)
    {
        if (low < high)
        {
            int pi = Particion(arr, low, high);
            Quicksort(arr, low, pi - 1);
            Quicksort(arr, pi + 1, high);
        }
    }

    static int Particion(int[] arr, int low, int high)
    {
        int pivot = arr[high];
        int i = low - 1;
        for (int j = low; j < high; j++)
        {
            if (arr[j] < pivot)
            {
                i++;
                (arr[i], arr[j]) = (arr[j], arr[i]);
            }
        }
        (arr[i + 1], arr[high]) = (arr[high], arr[i + 1]);
        return i + 1;
    }

    static void Heapsort(int[] arr)
    {
        int n = arr.Length;
        for (int i = n / 2 - 1; i >= 0; i--)
            Heapify(arr, n, i);
        for (int i = n - 1; i > 0; i--)
        {
            (arr[0], arr[i]) = (arr[i], arr[0]);
            Heapify(arr, i, 0);
        }
    }

    static void Heapify(int[] arr, int n, int i)
    {
        int largest = i, left = 2 * i + 1, right = 2 * i + 2;

        if (left < n && arr[left] > arr[largest])
            largest = left;
        if (right < n && arr[right] > arr[largest])
            largest = right;

        if (largest != i)
        {
            (arr[i], arr[largest]) = (arr[largest], arr[i]);
            Heapify(arr, n, largest);
        }
    }
}
