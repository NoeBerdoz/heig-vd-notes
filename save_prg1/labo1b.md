# Pseudo Code, LABO 1B
Gwenaël, Noé, Ophélie

## Inputs
- username = family name of the user
- accountNumber = account number of the user
- accountBalance (1000) = account balance in CHF
- exchangeRate (1.024) = 1 CHF to Euro exchange rate
- transactionFees (5) = money in CHF collected by the bank for a transaction
- withdrawalAmount = the money withdrawal by the user in Euro

- ticketColLeftWidth (18) = the label column width in character of the ticket
- ticketColRightWidth (9) = the result column width in character of the ticket
- ticketCorner ('+') = the character placed in each corner of the ticket
- ticketColSeparator (':') = the character placed to separate the two columns
- ticketColSeparatorWidth (1) = the number of character placed to separate the two columns
- ticketBorderVertical ('|') = the character used for the right and left borders
- ticketBorderHorizontal ('-') = the character used for the top and bottom borders
- ticketNumberPrecision (2) = the number of decimal used for the number precision except for the exchange rate

## Output
The formatted ticket with the following information:
- username
- account number
- withdrawal amount
- exchange rate
- converted withdrawal amount
- transaction fees
- final account balance

## Algorithm
```
ask accountNumber
ask username 

display accountBalance
display exchangeRate
display transactionFees

ask withdrawalAmount

calculate convertedWithdrawalAmount = withdrawalAmount / exchangeRate
calculate finalAccountBalance = accountBalance - convertedWithdrawalAmount - transactionFees

calculate ticketWidth = ticketColLeftWidth + ticketColRightWidth + ticketColSeparatorWidth

display as Ticket model
```

## Ticket model
+----------------------------+
|                            |
| TOTO                       |
| 1256845                    |
|                            |
| Somme Euro       :  125.00 |
| 1 CHF en Euro    :   1.024 |
|                            |
| Somme CHF        :  122.07 |
| Frais            :    5.00 |
|                            |
| Solde Compte     :  872.93 |
|                            |
+----------------------------+




/*------------------
Labo : 01B
Authors : Serex Ophélie, Ansermoz Gwenaël, Berdoz Noé
Goal : TODO
Creation Date : 04.10.2022
Modified: never
Comments : none
-----------------*/
#include <iostream>
#include <iomanip>

using namespace std;

const double EXCHANGE_RATE = 1.024;
const double TRANSACTION_FEES = 5;

const int TICKET_COL_LEFT_WIDTH = 18;
const int TICKET_COL_RIGHT_WIDTH = 9;
const char TICKET_CORNER = '+';
const char TICKET_COL_SEPARATOR = ':';
const int TICKET_COL_SEPARATOR_WIDTH = 1;
const char TICKET_BORDER_VERTICAL = '|';
const char TICKET_BORDER_HORIZONTAL = '-';
const int TICKET_NUMBER_PRECISION = 2;
const int TICKET_EXCHANGE_RATE_PRECISION = 3;

const int TICKET_WIDTH = TICKET_COL_LEFT_WIDTH + TICKET_COL_RIGHT_WIDTH + TICKET_COL_SEPARATOR_WIDTH;

int main() {
unsigned accountNumber = 0;
cout << "Quel est votre numéro de compte ?" << endl;
cin >> accountNumber;
cout << endl;


    string username;
    cout << "Quel est votre nom de famille ?" << endl;
    cin >> username;
    cout << endl;

    double accountBalance = 1000;

    cout << fixed << setprecision(TICKET_NUMBER_PRECISION);
    cout << "Solde de votre compte CHF : " << accountBalance << endl;

    cout << setprecision(TICKET_EXCHANGE_RATE_PRECISION);
    cout << "Taux de change : 1 CHF = " << EXCHANGE_RATE << " Euro" << endl;

    cout << setprecision(TICKET_NUMBER_PRECISION);
    cout << "Frais d’opération : " << TRANSACTION_FEES << " CHF" << endl;

    double withdrawalAmount= 0;
    cout << "Entrez la somme souhaitée en Euro :" << endl;
    cin >> withdrawalAmount;
    cout << endl;

    double convertedWithdrawalAmount = withdrawalAmount / EXCHANGE_RATE;
    double finalAccountBalance = accountBalance - convertedWithdrawalAmount - TRANSACTION_FEES;

    // Border top
    cout << TICKET_CORNER << setfill(TICKET_BORDER_HORIZONTAL) << setw(TICKET_WIDTH) << "" << TICKET_CORNER << endl;

    // Space
    cout << TICKET_BORDER_VERTICAL << setfill(' ') << setw(TICKET_WIDTH) << "" << TICKET_BORDER_VERTICAL << endl;

    // Username
    cout << TICKET_BORDER_VERTICAL << " " << left << setw(TICKET_WIDTH - 1) << username << TICKET_BORDER_VERTICAL << endl;

    // Account number
    cout << TICKET_BORDER_VERTICAL << " " << setw(TICKET_WIDTH - 1) << accountNumber << TICKET_BORDER_VERTICAL << endl;

    // Space
    cout << TICKET_BORDER_VERTICAL << setw(TICKET_WIDTH) << "" << TICKET_BORDER_VERTICAL << endl;

    // Withdrawal amount
    cout << TICKET_BORDER_VERTICAL << setw(TICKET_COL_LEFT_WIDTH) << " Somme Euro" << TICKET_COL_SEPARATOR << right
         << setw(TICKET_COL_RIGHT_WIDTH - 1) << withdrawalAmount << " " << TICKET_BORDER_VERTICAL << endl;

    // Exchange rate
    cout << setprecision(TICKET_EXCHANGE_RATE_PRECISION);
    cout << TICKET_BORDER_VERTICAL << left  << setw(TICKET_COL_LEFT_WIDTH) << " 1 CHF en Euro" << TICKET_COL_SEPARATOR
         << right << setw(TICKET_COL_RIGHT_WIDTH - 1) << EXCHANGE_RATE << " " << TICKET_BORDER_VERTICAL << endl;
    cout << setprecision(TICKET_NUMBER_PRECISION);

    // Space
    cout << TICKET_BORDER_VERTICAL << setw(TICKET_WIDTH) << "" << TICKET_BORDER_VERTICAL << endl;

    // Converted withdrawal amount
    cout << TICKET_BORDER_VERTICAL << left  << setw(TICKET_COL_LEFT_WIDTH) << " Somme CHF" << TICKET_COL_SEPARATOR
         << right << setw(TICKET_COL_RIGHT_WIDTH - 1) << convertedWithdrawalAmount << " " << TICKET_BORDER_VERTICAL
         << endl;

    // Transaction fees
    cout << TICKET_BORDER_VERTICAL << left  << setw(TICKET_COL_LEFT_WIDTH) << " Frais" << TICKET_COL_SEPARATOR << right
         << setw(TICKET_COL_RIGHT_WIDTH - 1) << TRANSACTION_FEES << " " << TICKET_BORDER_VERTICAL << endl;

    // Space
    cout << TICKET_BORDER_VERTICAL << setw(TICKET_WIDTH) << "" << TICKET_BORDER_VERTICAL << endl;

    // Final account balance
    cout << TICKET_BORDER_VERTICAL << left  << setw(TICKET_COL_LEFT_WIDTH) << " Solde Compte" << TICKET_COL_SEPARATOR
         << right << setw(TICKET_COL_RIGHT_WIDTH - 1) << finalAccountBalance << " " << TICKET_BORDER_VERTICAL << endl;

    // Space
    cout << TICKET_BORDER_VERTICAL << setw(TICKET_WIDTH) << "" << TICKET_BORDER_VERTICAL << endl;

    // Border bottom
    cout << TICKET_CORNER << setfill(TICKET_BORDER_HORIZONTAL) << setw(TICKET_WIDTH) << "" << TICKET_CORNER << endl;

    return 0;
}
