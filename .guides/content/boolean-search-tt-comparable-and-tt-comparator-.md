The repository for this book includes `Card.java`, which demonstrates two ways to sort a list of `Card` objects. Here's the beginning of the class definition:

\begin{verbatim}
public class Card implements Comparable<Card> {

    private final int rank;
    private final int suit;

    public Card(int rank, int suit) {
        this.rank = rank;
        this.suit = suit;
    }
\end{verbatim}

A `Card` object has two integer fields, `rank` and `suit`. `Card` implements `Comparable<Card>`, which means that it provides `compareTo`:

\begin{verbatim}
    public int compareTo(Card that) {
        if (this.suit < that.suit) {
            return -1;
        }
        if (this.suit > that.suit) {
            return 1;
        }
        if (this.rank < that.rank) {
            return -1;
        }
        if (this.rank > that.rank) {
            return 1;
        }
        return 0;
    }
\end{verbatim}


The specification of `compareTo` indicates that it should return a negative number if `this` is considered less than `that`, a positive number if it is considered greater, and 0 if they are considered equal.

If you use the one-parameter version of `Collections.sort`, it uses the `compareTo` method provided by the elements to sort them. To demonstrate, we can make a list of 52 cards like this:

\begin{verbatim}
    public static List<Card> makeDeck() {
        List<Card> cards = new ArrayList<Card>();
        for (int suit = 0; suit <= 3; suit++) {
            for (int rank = 1; rank <= 13; rank++) {
                Card card = new Card(rank, suit);
                cards.add(card);
            }
        }
        return cards;
    }
\end{verbatim}

And sort them like this:

\begin{verbatim}
        Collections.sort(cards);
\end{verbatim}

This version of `sort` puts the elements in what's called their “natural order” because it's determined by the objects themselves.


But it is possible to impose a different ordering by providing a `Comparator` object. For example, the natural order of `Card` objects treats Aces as the lowest rank, but in some card games they have the highest rank. We can define a `Comparator` that considers “Aces high”, like this:

\begin{verbatim}
        Comparator<Card> comparator = new Comparator<Card>() {
            @Override
            public int compare(Card card1, Card card2) {
                if (card1.getSuit() < card2.getSuit()) {
                    return -1;
                }
                if (card1.getSuit() > card2.getSuit()) {
                    return 1;
                }
                int rank1 = getRankAceHigh(card1);
                int rank2 = getRankAceHigh(card2);

                if (rank1 < rank2) {
                    return -1;
                }
                if (rank1 > rank2) {
                    return 1;
                }
                return 0;
            }

            private int getRankAceHigh(Card card) {
                int rank = card.getRank();
                if (rank == 1) {
                    return 14;
                } else {
                    return rank;
                }
            }
        };
\end{verbatim}

This code defines an anonymous class that implements `compare`, as required. Then it creates an instance of the newly-defined, unnamed class. If you are not familiar with anonymous classes in Java, you can read about them at [http://thinkdast.com/anonclass](http://thinkdast.com/anonclass).


Using this `Comparator`, we can invoke `sort` like this:

\begin{verbatim}
        Collections.sort(cards, comparator);
\end{verbatim}

In this ordering, the Ace of Spades is considered the highest class in the deck; the two of Clubs is the lowest.


The code in this section is in `Card.java` if you want to experiment with it. As an exercise, you might want to write a comparator that sorts by `rank` first and then by `suit`, so all the Aces should be together, and all the twos, etc.