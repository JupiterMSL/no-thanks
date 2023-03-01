# no-thanks
317 and 307 usm stuff
//Author Mason Lee
// this program simulates a race between the tortoise and the hare.


using System;
using System.Threading;

abstract class RaceAnimal
{
    protected char[] track = new char[70];
    protected char symbol;
    public int position;  // change access modifier to public
    protected string name;

    public RaceAnimal(string name, char symbol)
    {
        this.name = name;
        this.symbol = symbol;

        // initialize the track with dashes
        for (int i = 0; i < track.Length; i++)
        {
            track[i] = '-';
        }

        // place the animal symbol at the start of the track
        track[0] = symbol;
        position = 0;
    }

    public override string ToString()
    {
        return new string(track);
    }

    protected void ChangePos(int steps)
    {
        int newPos = position + steps;

        // check bounds to ensure the move is in bounds
        if (newPos < 0)
        {
            newPos = 0;
        }
        else if (newPos > 69)
        {
            newPos = 69;
        }

        // update track with new position
        track[position] = '-';
        position = newPos;
        track[position] = symbol;
    }

    public abstract void Move();
}


class Tortoise : RaceAnimal
{
    public Tortoise() : base("Tortoise", 'T') { }

    public override void Move()
    {
        int moveType = new Random().Next(1, 11);

        if (moveType <= 5)
        {
            ChangePos(3);
        }
        else if (moveType <= 7)
        {
            ChangePos(-6);
        }
        else
        {
            ChangePos(1);
        }

        Thread.Sleep(1000);
    }
}

class Hare : RaceAnimal
{
    public Hare() : base("Hare", 'H') { }

    public override void Move()
    {
        int moveType = new Random().Next(1, 11);

        if (moveType <= 2)
        {
            ChangePos(0);
        }
        else if (moveType <= 4)
        {
            ChangePos(9);
        }
        else if (moveType == 5)
        {
            ChangePos(-12);
        }
        else if (moveType <= 8)
        {
            ChangePos(1);
        }
        else
        {
            ChangePos(-2);
        }

        Thread.Sleep(1000);
    }
}

class Race
{
    private Tortoise tortoise;
    private Hare hare;

    public Race()
    {
        tortoise = new Tortoise();
        hare = new Hare();
    }

    public void Simulate()
    {
        Console.WriteLine("BANG !!!!");
        Console.WriteLine("AND THEY'RE OFF !!!!!");

        while (true)
        {
            tortoise.Move();
            hare.Move();

            Console.WriteLine(tortoise);
            Console.WriteLine(hare);

            if (tortoise.position >= 69 || hare.position >= 69)
            {
                break;
            }
        }

        if (tortoise.position >= 69 && hare.position >= 69)
        {
            Console.WriteLine("It's a tie!");
        }
        else if (tortoise.position >= 69)
        {
            Console.WriteLine("Tortoise wins!");
        }
        else
        {
            Console.WriteLine("Hare wins!");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        Race race = new Race();
        race.Simulate();
    }
}
