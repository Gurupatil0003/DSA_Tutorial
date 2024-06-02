# Basic Theory
There are two kinds of data types, namely:
- Standard data type
  That is the type of data that has been defined by the compiler that can directly be declared when needed. Examples such as `int`, `float`, `char`, `double`, `void`.
- User defined data type
  That data types defined by the user according to his needs. The first step is to define or create the desired data type first, then declare variables with these data types. Examples like `struct` and `union`.

Structure (`struct`) is a set of data which may be different data types that use the same name and is distinguished through its field name. Thus it is possible a structure contains elements of different data types such as `char`, `int`, `float`, `double`, and others.

Structure is defined using the `struct` keyword. Here's an example of defining a data type structure:
```c
struct date 
{
	int month;
	int day;
	int year;
};
```
or
```c
struct date 
{
	int month, day, year
};
```

The examples above are the establishment of a new data type called `struct date` that has three elements (*fields*) in the form of `month`, `day`, and `year`.

Here is the other example
```c
struct date today;
```
The statement above states that a variable of type struct date today.

In defining a structure, the elements contained in them can also be a structure. Example:
```c
struct date 
{
	int month, day, year;
};

struct student 
{
	char name[30];
	struct date birthday;
};

struct student mhs;
```

Data structure diagram of a variable `mhs` can be described as follows:

![Image of Diagram](https://github.com/rizalasrul/c-basic-struct/blob/master/Images/1.png)

Elements of a structure variable can be accessed by mentioning the name of the structure variable followed by the dot operator ('.') And the name of the element structure. The way of writing as follows:
```c
struct_variable.field_name;
```

For example, provide the data field name to the name of the variable `student` above, then the statement is required, for example is:
```c
strcpy(mhs.name, “BUDI”);
```

The following example is an instruction to fill in the data field `birthday`:
```c
mhs.birthday.day = 10;
```

Meanwhile, to get the contents of a field of variable structure, for example: `date = mhs.birthday.day;` an instruction to deliver the content of the field day to a date variable. `puts (mhs.name);` an on-screen instructions to display the contents of the name field.

A structure can also be initialized when declared. This is similar to the array initialization, the elements are written in a pair of curly braces ('{}') with each separated by a comma.

Examples for variable `mhs` above:
```c
struct strudent mhs = {“Rizal”, 4, 11, 1993};
```


# How This Code Work
## `struct1.c`
Code

```c
#include <stdio.h>
#define MAKS 20

struct date {
	int month, day, year;
};
struct student {
	char name[30];
	struct date birthday;
};

main() {
	struct student data_mhs[MAKS];
	int i = 0, jml;
	char lagi;

	do {
		printf("Name : ");
		gets(data_mhs[i].name);
		printf("Birthday (mm-dd-yyyy): ");
		scanf("%d-%d-%d", 
			&data_mhs[i].birthday.month,
			&data_mhs[i].birthday.day,
			&data_mhs[i].birthday.year);
		i++;
		fflush(stdin);
		printf("\nMau memasukkan data lagi [Y/T]? ");
		lagi = getchar();
		fflush(stdin);
	} while (lagi == 'Y' || lagi == 'y');

	jml = i;
	printf("\nDATA MAHASISWA\n");
	for (i = 0; i < jml; i++) {
		printf("%d. Name\t: %s", i + 1, data_mhs[i].name);
		printf("\n   Birhtday\t: %d=%d-%d\n\n",
			data_mhs[i].birthday.month,
			data_mhs[i].birthday.day,
			data_mhs[i].birthday.year);
	}
}
```
Capture Output

![Image of Diagram](https://github.com/rizalasrul/c-basic-struct/blob/master/Images/2.png)

The program will display data from students who have input by the user. A broad set several variables, namely `data_mhs` variable type `array of struct student` where data type `struct student` contains the name variable of type `array of char` and `birthday` date data type struct where struct data types date itself contains variables month, day, and year integers. Then there's the variable i as the index array of integers, variables bouli to help display the output type integer, and again for the looping variable of type char.

The data type struct student used to accommodate input from the user because the data types are struct student as a container field name student name and birthday field to accommodate the student's date of birth. So that at the end of the program, needs to be displayed is simply a variable with the data type struct student with the field name and birthday.

## `struct2.c`
```c
#include <stdio.h>

main() {
	struct date {
		int day, month, year;
	} today, tomorrow;
	
	puts("MENCARI NILAI TANGGAL");
	fflush (stdin);
	printf("\nMasukkan tanggal sekarang [dd-mm-yyyy): ");
	scanf("%d-%d-%d", &today.day, &today.month, &today.year);
	tomorrow = today;
	tomorrow.day++;
if (today.month == 1 || today.month == 3 || today.month == 5 || today.month == 7 || today.month == 8 || today.month == 10 || today.month == 12) {
		if (today.day == 31) {
			if (today.month == 12)
tomorrow.day = 1, tomorrow.month = 1, tomorrow.year++;
			else
				tomorrow.day = 1, tomorrow.month++;
		}
	}
	else {
		if (today.month == 2) {
			if (today.year % 4 != 0) {
				if (today.day == 28)
					tomorrow.day = 1, tomorrow.month++;
			}
			else {
				if (today.day == 29)
					tomorrow.day = 1, tomorrow.month++;
			}
		}
		else 
			if (today.day == 30)
				tomorrow.day = 1, tomorrow.month++;
	}
printf("Besoknya: %d-%d-%d\n", tomorrow.day, tomorrow.month, tomorrow.year);
}
```
Capture Output

![Image of Diagram](https://github.com/rizalasrul/c-basic-struct/blob/master/Images/3.png)

The program will display a date after the date that the user entered. Tomorrow and today there are variables with data type struct date that has a field day, month, and year integers.

The first user will be inputting-kan a date and stored in the variable today. Then assign the value of the variable today to tomorrow. Then the process tomorrow.day ++. Then do the checking process. If the month-on-input is the same as in January, March, May, July, August, October, and December, then be checked again. If the day on-the-input equal to 31, then be checked again. If the month at-the-input equal to 12, then the process tomorrow.day = 1, tomorrow.month = 1, tomorrow.year ++. If it is not equal to 12, then the process tomorrow.day = 1, tomorrow.month ++.

And if the moon is in the input-is the same as in February, April, June, September, and November, then be checked again. If the month-on-input is the same as in February, then do the checking process again. If the year is entered is not a leap year (it can not be divided by 4), then be checked again. If the day is entered equal to 28, then the process tomorrow.day = 1, tomorrow.month ++. But if the year entered is a leap year, then be checked again. If the day is included is 29, then the process tomorrow.day = 1, tomorrow.month ++. But if the moon entered not in February, then do check back. If the day is included is 30, then the process tomorrow.day = 1, tomorrow.month ++. Then show tomorrow variables with each of the field.

## `struct3.c`
```c
#include <stdio.h>
#include <string.h>

main() {
	struct GFC {
		char kind;
		char food[6];
		int price, qty, sum;
	} order[15];
	int i = 0, tempcount, total = 0, fee;
	char option;

	puts("Toko GFC - Gerobak Fried Chicken\n");
	puts("DAFTAR HARGA");
	puts("Kode\tJenis\tHarga Per Potong");
	puts("D\tDada\tRp. 5000.00");
	puts("P\tPaha\tRp. 4000.00");
	puts("S\tSayap\tRp. 3000.00\n");
	puts("Harga belum termasuk pajak : 10%\n");
	puts("Masukkan Pesanan Anda");
	do {
		printf("Pesanan ke-%d\n", i + 1);
		fflush(stdin);
		printf("Jenis [D/P/S]\t: ");
		scanf("%c", &order[i].kind);
		fflush(stdin);
		printf("Jumlah\t\t: ");
		scanf("%d", &order[i].qty);
		fflush(stdin);
		printf("Ada lagi <Y/T>? ");
		option = getchar();
		fflush(stdin);
		if (order[i].kind == 'D' || order[i].kind == 'd') {
			strcpy(order[i].food,"DADA");
			order[i].price = 5000;
		}
		else if (order[i].kind == 'P' || order[i].kind == 'p') {
			strcpy(order[i].food,"PAHA");
			order[i].price = 4000;
		}
		else {
			strcpy(order[i].food,"SAYAP");
			order[i].price = 3000;
		}
		order[i].sum = order[i].qty * order[i].price;
		total += order[i].sum;
		i++;
		puts("");
	} while (option == 'y' || option == 'Y');
	tempcount = i;
	fee = total / 10;
	puts("\nNota Belanja Anda :\n");
	puts("\t\tGEROBAK FRIED CHICKEN\n");
puts("============================================================");
	puts("No\tJenis Potong\tHarga Satuan\tQty\tJumlah Harga");
puts("============================================================");
	for (i = 0; i < tempcount; i++) {
		printf("%d\t%s\t\tRp.%6d.00\t%d\tRp.%6d.00\n", i + 1,
			order[i].food,
			order[i].price,
			order[i].qty,
			order[i].sum);
	}
puts("============================================================");
	printf("\t\t\t\tJumlah Bayar\tRp.%6d.00\n", total);
	printf("\t\t\t\tPajak 10%%\tRp.%6d.00\n", fee);
	printf("\t\t\t\tTOTAL BAYAR\tRp.%6d.00\n", total + fee);
}
```
Capture Output

![Image of Diagram](https://github.com/rizalasrul/c-basic-struct/blob/master/Images/4.png)

![Image of Diagram](https://github.com/rizalasrul/c-basic-struct/blob/master/Images/5.png)

The program will display a menu where the user can order from the menu ditampilan program and the program can also display the purchase orders from the user. The variables used were the order type array of struct GFC, where struct GFC has a field be kind to accommodate characters from the type menu of type char, food to accommodate the name of the type of menu type array of char, price to the price of each menu integers, qty for the quantity of type integer, and the total sum to accommodate the times field price and qty as the total price per menu. There are also variable i initialization 0 to array index, tempcount for setting the memorandum, the total initialization 0 as the overall price to be paid, the fee for the tax, and each of these variables of type integer. Then there is a variable of type char option for looping.

The first user will enter a variable order with kind and qty field with index-i. Then enter the variable option. If the variable order with the kind field to index-i is equal to 'D' or 'd', then the string "DADA" will be copied ¬ke order with a variable field of food with the help of strcpy (), and variable order with a price field will be initialized by 5000. But if the variable order with the kind field to index-i is equal to 'P' or 'p', then the string "thigh" will be copied to the variable order with the field of food and price variable order with the field will be initialized with 4000 . But if the order with a variable index-field kind i do not meet the above requirements, then the string "WINGS" will be copied to the variable order with the field of food and price variable order with the field will be initialized by 3000. then the process order [i] .sum = order [i] .qty * order [i] .price and total + = order [i] .sum. Then the i ++. If the option is equal to 'Y' or 'y', then repeat all of the above process.
