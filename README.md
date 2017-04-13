# BookStore

var listOfAllKnownAuthors = []

// creating class for BookStore
class BookStore
{
    constructor(name, address, owner)
	{
        this._name = name;
        this._address = address;
        this._owner = owner;
        this._booksAvailable = [];
        this._numTitles = 0
        this._totalCopiesOfAllBooks = 0
    }

    authorKnown(authorName)
	{
        var foundThem = false;
        for (var pos = 0; pos < listOfAllKnownAuthors.length; pos++)
		{
            if (authorName === listOfAllKnownAuthors[pos])
			{
                foundThem = true
            }
        }
        return foundThem
    }

    addBook(bookInstance, copies){
        var positionOfBook = this.checkForBook(bookInstance);
        if (positionOfBook != null){
             this._booksAvailable[positionOfBook].copies += copies;
             console.log("Added "+ copies + " copies of "+ bookInstance);
             listOfAllKnownAuthors.push(bookInstance.author);
        }
        else {
             var BookCopies = {
                 Book:bookInstance,
                 Copies:copies
             };
             this._booksAvailable.push(BookCopies);
             this._numTitles += 1;
             console.log("Added " + copies + " copies of a new book: " + bookInstance);
        }

        this._totalCopiesOfAllBooks += copies;
    }

    sellBook(bookInstance, numberSold)
	{
        var positionOfBook = this.checkForBook(bookInstance);
        if (positionOfBook != null)
		{
            if (numberSold > this._booksAvailable[positionOfBook].copies)
			{
                console.log("not enough copies of "+BookInstance+" to sell");
            }
            else
			{
                this._booksAvailable[positionOfBook].copies -= numberSold;
                if (this._booksAvailable[positionOfBook].copies===0)
				{
                    this._booksAvailable.pop(PositionOfBook);
                    this._NumTitles -= 1;
                    var foundAuth = this.AuthorKnown(BookInstance.GetAuthor());
                    listOfAllKnownAuthors.pop(foundAuth);
                }
                this._totalCopiesOfAllBooks -= numberSold;
                console.log("sold " + numberSold + " copies of " + bookInstance);
            }
        }
        else
		{
            console.log(bookInstance.toString() + " not found")
        }
    }

    checkForBook(bookInstance)
	{
        var currBookNum = 0;
        var found = false;
        var foundPos = null;
        while (currBookNum < this._numTitles)
		{
            if (this._booksAvailable[currBookNum].Book === bookInstance)
			{
                found = true;
                foundPos = currBookNum;
            }
            else
			{
                found = false;
                foundPos = null;
            }
            currBookNum += 1;
        }
        return foundPos;
    }

    get name()
	{
        return this._name;
    }

    set name(newName)
	{
        this._name = newName;
    }

    get address()
	{
        return this._address;
    }

    set address(newAddress)
	{
        this._address = newAddress;
    }

    get owner()
	{
        return this._owner;
    }

    set address(newOwner)
	{
        this._owner = newOwner;
    }
}

class Book
{
    constructor(title, author, publicationYear, price)
	{
        this._title = title;
        this._author = author;
        this._publicationYear = publicationYear;
        this._price = price;
        if (this.authorKnown(this._author) === false)
		{
            listOfAllKnownAuthors.push(this._author)
        }
    }

    authorKnown(authorName)
	{
        var foundThem = false;
        for (var pos = 0; pos < listOfAllKnownAuthors.length; pos++)
		{
            if (authorName === listOfAllKnownAuthors[pos])
			{
                foundThem = true;
            }
        }
        return foundThem;
    }

    get title()
	{
        return this._title;
    }

    get author()
	{
        return this._author;
    }

    get publicationYear()
	{
        return this._publicationYear;
    }

    get price()
	{
        return this._price;
    }

	toString()
	{
        return this.title + ", " + this.author + ". " + this.publicationYear + " ($" + this.price + ")";
    }
}

// Book details courtesy of Harry Potter series by J.K. Rowling

var FlourishAndBlotts = new BookStore("Flourish &amp; Blotts","North side, Diagon Alley, London, England","unknown")
var MonsterBook = new Book("The Monster Book of Monsters","Edwardus Lima",1978,40)
var MonsterBookToSell = new Book("The Monster Book of Monsters","Edwardus Lima",1978,40)
FlourishAndBlotts.addBook(MonsterBook,500)
FlourishAndBlotts.sellBook(MonsterBookToSell,200)
var SpellBook = new Book("The Standard Book of Spells, Grade 4","Miranda Goshawk",1921, 80)
FlourishAndBlotts.addBook(SpellBook,40)
FlourishAndBlotts.addBook(SpellBook,20)
FlourishAndBlotts.sellBook(SpellBook,15)
FlourishAndBlotts.addBook(MonsterBookToSell,30)

console.log("authors known: "+listOfAllKnownAuthors)
