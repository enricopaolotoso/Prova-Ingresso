using System;
using System.Collections.Generic;
using System.Linq;

namespace ProvaIngresso
{
    enum tipoCombustibile { gas, luce }

    class Impianto
    {
        public double rendimento, bolletta, spesaFissa, energiaProdotta;
        tipoCombustibile tipo;

        public string nome;

        public Impianto(double rendimento, double spesaFissa, tipoCombustibile tipo, string nome) //costruttore
        {
            this.rendimento = rendimento; //dichiaro l'attributo inserendo il valore dal main
            this.spesaFissa = spesaFissa;
            this.tipo = tipo;
            this.nome = nome;
        }

        public double Rendimento { get => rendimento; set => rendimento = value; } //prendo il valore e lo inizializzo
        public double Bolletta { get => bolletta; set => bolletta = value; }

        public void CalcolaSpeseConsumi(in double consumo, in double prezzo) //calcolo spese e consumi
        {
            this.bolletta = Math.Round((consumo * prezzo) + spesaFissa, 4); //calolo bolletta generale
            if (this.tipo == tipoCombustibile.gas)
            {
                this.energiaProdotta = Math.Round(consumo * 8 * this.rendimento); //1smc di gas fornisce 8 kWh termici
            }
            else
            {
                this.energiaProdotta = Math.Round(consumo * 4 * this.rendimento); //1kWh di luce fornisce 4 kWh termici
            }
        }

        public override string ToString() //formattazione e visualizzazione stringa
        {
            return $"Il metodo più conveniente è: {this.nome } con un costo annuale di {this.bolletta} € ";
        }
    }


    class Program
    {

        static void Main(string[] args)
        {
            int decisione = 0; //dichiarazione variabili
            double consumogas; 
            double consumoluce;
            const double prezzogas = 1.08;
            const double prezzoluce = 0.276;
            string risposta, metodo = "";
            bool controllo;

            Impianto caldaiatradizionale = new Impianto(0.9, 213, tipoCombustibile.gas, "caldaia tradizionale");
            Impianto caldaiacondensazione = new Impianto(1, 213, tipoCombustibile.gas, "caldaia a condensazione");
            Impianto stufaelettrica = new Impianto(1, 0, tipoCombustibile.luce, "stufa elettrica");
            Impianto pompacalorebuona = new Impianto(3.6, 3000, tipoCombustibile.luce, "pompa a calore buona");
            Impianto pompacaloreeco = new Impianto(2.8, 1000, tipoCombustibile.luce, "pompa a calore economica");

            Console.WriteLine("Inserire il  proprio consumo annuo di gas in Smc:"); //input 
            consumogas = Convert.ToDouble(Console.ReadLine());

            Console.WriteLine("Inserire il proprio consumo annuo di luce in kwH:");
            consumoluce = Convert.ToDouble(Console.ReadLine());


            do
            {
                Console.WriteLine("Scegli il tuo metodo di riscaldamento\n" +
                              "Digita 1 per la caldaia tradizionale\n" +
                              "Digita 2 per la caldaia a condensazione\n" +
                              "Digita 3 per la stufa elettrica\n" +
                              "Digita 4 per la pompa di calore economica\n" +
                              "Digita 5 per pompa di calore di buon livello\n");

                risposta = Convert.ToString(Console.ReadLine());
                controllo = int.TryParse(risposta, out decisione); // controllo se il tipo di dato inserito è int
            } while (!controllo || decisione < 1 || decisione > 5); // Leggo il metodo attualmento installato (possibilità di scelta 1-5)

            switch (decisione) //associo il numero al metodo selezionato
            {
                case 1:
                    metodo = "caldaia tradizionale";
                    break;
                case 2:
                    metodo = "caldaia a condensazione";
                    break;
                case 3:
                    metodo = "stufa elettrica";
                    break;
                case 4:
                    metodo = "pompa a calore buona";
                    break;
                case 5:
                    metodo = "pompa a calore economica";
                    break;

            }

            Calcolatore(ref caldaiatradizionale, ref caldaiacondensazione, ref stufaelettrica, ref pompacalorebuona, //calcolo valori 
            ref pompacaloreeco, consumogas, consumoluce, prezzogas, prezzoluce);

            
            List<Impianto> metodi = new List<Impianto>() { caldaiatradizionale, caldaiacondensazione, stufaelettrica, pompacalorebuona, pompacaloreeco }; //lista che contiene tutti gli impianti
            metodi = metodi.OrderBy(m => m.Bolletta).ToList();

            if (metodi[0].nome == metodo) //stampo a video il metodo più conveniente
            {
                Console.WriteLine("\nIl metodo più conveniente corrisponde a quello già installato");
            }
            else
            {
                Console.WriteLine($"\n{metodi[0].ToString()}");
            }

            Console.ReadKey();



        }

        //raggruppo le chiamate del metodo per calcolare spese e consumi
        static void Calcolatore(ref Impianto caldaiatradizionale, ref Impianto caldaiacondensazione, ref Impianto stufaelettrica,
            ref Impianto pompacalorebuona, ref Impianto pompacaloreeco, in double consumogas, in double consumoluce, in double prezzogas, in double prezzoluce)
        {
            caldaiatradizionale.CalcolaSpeseConsumi(consumogas, prezzogas);
            caldaiacondensazione.CalcolaSpeseConsumi(consumogas, prezzogas);
            stufaelettrica.CalcolaSpeseConsumi(consumoluce, prezzoluce);
            pompacalorebuona.CalcolaSpeseConsumi(consumoluce, prezzoluce);
            pompacaloreeco.CalcolaSpeseConsumi(consumoluce, prezzoluce);
        }

    }
}