# LV2
Laboratorijske vježbe 2 - RPPOON

Zadatak 1. Kreirajte objekt klase DiceRoller i u njega ubacite 20 kockica. Baciti sve kockice i ispisati rezultate bacanja kockica na ekran.

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace LV2-Zad1
{

class Die
    {
    
        private int numberOfSides; 
        private Random randomGenerator;

        public Die(int numberOfSides) 
        { 
            this.numberOfSides = numberOfSides; 
            this.randomGenerator = new Random(); 
        }

        public int Roll() {
            int rolledNumber = randomGenerator.Next(1, numberOfSides + 1);
            return rolledNumber; 
        }
    }
class DiceRoller
    {
    
        private List<Die> dice;
        private List<int> resultForEachRoll; 
 
        public DiceRoller()         
        {             
            this.dice = new List<Die>(); 
            this.resultForEachRoll = new List<int>();    
        }
        public DiceRoller(int numberOfDices)
        {
            this.dice = new List<Die>(numberOfDices);
            this.resultForEachRoll = new List<int>();
        }
 
        public void InsertDie(Die die)  
        {            
            dice.Add(die);   
        } 
 
        public void RollAllDice()
        {        
            this.resultForEachRoll.Clear();       
            foreach (Die die in dice)       
            {          
                this.resultForEachRoll.Add(die.Roll());  
            }    
        } 

        public IList<int> GetRollingResults()     
        {        
            return new System.Collections.ObjectModel.ReadOnlyCollection<int> 
                ( this.resultForEachRoll );      
        } 
 
        public int DiceCount     
        {         
            get {
                return dice.Count;
            }    
        }
    }
    
class Program
    {
    
        static void Main(string[] args)
        {
            DiceRoller dice = new DiceRoller(20);
            
            for( int i=0; i<20;i++)
            {
                dice.InsertDie(new Die(6));
            }
            
            dice.RollAllDice();
            
            IList<int> results = dice.GetRollingResults();
            
            foreach (int result in results)
            {
                Console.WriteLine(result);
            }
        }
    }
}
    
Zadatak 2. Izmijeniti klasu Die tako da joj se preko konstruktora predaje generator pseudo-slučajnih brojeva. Ponoviti zadatak 1. 

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace LV2-Zad2
{

class Die
    {
    
        private int numberOfSides;
        private Random randomGenerator;

        public Die(int numberOfSides, Random randomGenerator)
        {
            this.numberOfSides = numberOfSides;
            this.randomGenerator = randomGenerator;
        }

        public int Roll()
        {
            int rolledNumber = randomGenerator.Next(1, numberOfSides + 1);
            return rolledNumber;
        }
    }
    
class DiceRoller
    {
    
        private List<Die> dice;
        private List<int> resultForEachRoll;

        public DiceRoller()
        {
            this.dice = new List<Die>();
            this.resultForEachRoll = new List<int>();
        }
        public DiceRoller(int numberOfDices)
        {
            this.dice = new List<Die>(numberOfDices);
            this.resultForEachRoll = new List<int>();
        }

        public void InsertDie(Die die)
        {
            dice.Add(die);
        }

        public void RollAllDice()
        {
            this.resultForEachRoll.Clear();
            foreach (Die die in dice)
            {
                this.resultForEachRoll.Add(die.Roll());
            }
        }

        public IList<int> GetRollingResults()
        {
            return new System.Collections.ObjectModel.ReadOnlyCollection<int>
                (this.resultForEachRoll);
        }

        public int DiceCount
        {
            get
            {
                return dice.Count;
            }
        }
    }
    
class Program
    {
    
        static void Main(string[] args)
        {
            DiceRoller dice = new DiceRoller(20);

            Random randomNumber = new Random();
            for( int i=0; i<20;i++)
            {
                dice.InsertDie(new Die(6,randomNumber));
            }
            dice.RollAllDice();
            IList<int> results = dice.GetRollingResults();
            foreach (int result in results)
            {
                Console.WriteLine(result);
            }
        }
    }
}

