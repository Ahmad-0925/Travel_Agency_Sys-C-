# Travel_Agency_Sys-C-




#include <iostream>
using namespace std;

struct pkg {
	string place, sdate, edate;  // sdate=start date.....edate=end date//
	int p, tickets;                      // price of pkg
};




///==============FUNCTIONS==========///
void mydetails(){
	cout << "......TRAVEL AGENCY SYSTEM......" << endl;
	cout << "NAME:AHMAD - HASSAN" << endl;
	cout << "Section: BSCS GC (1B)" << endl;
	cout << "ARID NO:2024-Arid-3793" << endl;
	cout << "Submitted to: MA'AM MONA" << endl;
	cout << "SUBJECT: Programming Fundamentals" << endl;
}



void packages(pkg a, pkg b, pkg c) {												///PACKAGES///
	cout << "\t\t\t\t============= TOUR PLACES & PLANS =============" << endl;
	cout << "\n\t\t\t[------- Details of Package 1 -------]\n";
	cout << "\t\t\tPlace: " << a.place << "\n\t\t\tStart date: " << a.sdate << "\n\t\t\tEnd date: " << a.edate << "\n\t\t\tPrice: Rs " << a.p;
	cout << "\n\n\t\t\t[------- Details of Package 2 -------]\n";
	cout << "\t\t\tPlace: " << b.place << "\n\t\t\tStart date: " << b.sdate << "\n\t\t\tEnd date: " << b.edate << "\n\t\t\tPrice: Rs " << b.p;
	cout << "\n\n\t\t\t[------- Details of Package 3 -------]\n";
	cout << "\t\t\tPlace: " << c.place << "\n\t\t\tStart date: " << c.sdate << "\n\t\t\tEnd date: " << c.edate << "\n\t\t\tPrice: Rs " << c.p;
}

void menu() {
	cout << "\n\nChoose an option:\n";												///MENU///
	cout << "1. Book a Package\n";
	cout << "2. Show Bookings\n";
	cout << "3. Cancel Bookings\n";
	cout << "4. Search Bookings\n";
	cout << "5. Exit\n";

}

int add_bookings(int ct, int choiceagain, int tkts, pkg bookings[], pkg a, pkg b, pkg c) {
	if (ct < 100) { //ct<100 means jb tk booking <100 he tb tk wo pkg choose kr skta //
		cout << "Choose a package:\n1. Package 1 (India)\n2. Package 2 (Kashmir)\n3. Package 3 (Timbaktu)\n";
		cin >> choiceagain; // choice again bnai he ta k upr book package wali choice entr krne k bd choice li jaye k usne kdr jana///
		while (choiceagain < 1 || choiceagain > 3) {// ye bs invalid choice k liye loop ta k user sai press kre glti hojati button press hjta//
			cout << "Invalid input. Enter 1, 2, or 3 for your package: ";
			cin >> choiceagain;
		}
		cout << "Enter the number of tickets (1 to 5): ";
		cin >> tkts;
		while (tkts < 1 || tkts > 5) {// ye bs invalid choice k liye loop ta k user sai press kre glti hojati button press hjta//
			cout << "Invalid ticket number. Enter between 1 and 5: ";
			cin >> tkts;
		}

		int totalp = 0;  //
		if (choiceagain == 1) {

			totalp = a.p * tkts;
			a.tickets = tkts;
			bookings[ct] = a;  // ct is booking no. here or ye bookings k index me store hojaega agr wo 1st book idnia krta .....
		}
		else if (choiceagain == 2) {
			b.tickets = tkts;
			totalp = b.p * tkts;
			bookings[ct] = b;  //  same here but for kashmir 
		}
		else if (choiceagain == 3) {
			c.tickets = tkts;
			totalp = c.p * tkts;
			bookings[ct] = c;  // and her for timbaktu//
		}
		cout << "You booked " << tkts << " ticket(s) for " << bookings[ct].place << ". Total price: Rs " << totalp << ".\n";
		ct++;
		return ct;
	}
	else {
		cout << "ur booking limit is full delete any booking to add a new one.\n";
		return ct;
	}
}
void displaying(int ct, pkg bookings[]) {
	if (ct > 0) { // ct>0 isliye agr booking hogi too kuch show ho wrna else chaly is if kaa
		cout << "\n\t\t\t\tBooking Details:\n";
		int total_booking_price = 0; // ye bs btayega total booking ktni krli user ne use add kr kr k jb jb
		for (int i = 0; i < ct; i++) {  // i <ct isiye ta k sirf wohi show hon jo add hui...// koi number dala ya 99 too garbage value dega
			int ticket_price = bookings[i].tickets * bookings[i].p;
			cout << "\n\t\t\tBooking=  " << i + 1;
			cout << "\n\t\t\tPlace: " << bookings[i].place << "\n\t\t\tStart Date: " << bookings[i].sdate << "\n\t\t\tEnd Date: "
				<< bookings[i].edate << "\n\t\t\tPrice: Rs " << bookings[i].p << "\n\t\t\tTickets for this tour=" << bookings[i].tickets << endl;
			cout << "total price of tickets=" << ticket_price << endl;
			total_booking_price = total_booking_price + ticket_price;

		}
		cout << "\n\nTotal Price for all bookings: Rs " << total_booking_price << ".\n\n";

	}
	else {
		cout << "No bookings yet. Add one or more to view details.\n";
	}
}

int cancelling(int ct, pkg bookings[]) {

	if (ct > 0) {
		int cancel;
		cout << " tell me cancel which booking??";
		cin >> cancel;
		while (cancel < 1 || cancel > ct) {
			cout << "Invalid choice. Enter a valid booking number: ";
			cin >> cancel;
		}
		int cid = -1;     /// cancel booking index ///
		for (int i = 0;i < ct;i++) {
			if (i == cancel - 1) { cid = i; break; } /// if 100 cancel input then cancel is 100-1=99 ///
		}


		if (cid != -1) {
			for (int i = cid;i < ct - 1;i++) {
				bookings[i] = bookings[i + 1];
				cout << "booking" << bookings[i].place << endl
					<< bookings[i].sdate << endl
					<< bookings[i].edate << endl
					<< bookings[i].p << endl;
			}
			ct--;
			cout << "ur booking" << cancel << "is canceled";
			return ct;
		}
		else { cout << "Such booking doesnot exist"; return ct; }
	}
}


void searching(int ct, pkg bookings[]) {
	string search;
	cout << "Enter the Booking Place Name for Search =";
	cin >> search;

	int bookingfound = -1;
	for (int i = 0; i < ct; i++)
	{
		if (search == bookings[i].place)
		{
			int ticket_price = bookings[i].tickets * bookings[i].p;
			bookingfound = i;
			break;
			cout << "\n\t\t\tPlace: " << bookings[i].place << "\n\t\t\tStart Date: " << bookings[i].sdate << "\n\t\t\tEnd Date: "
				<< bookings[i].edate << "\n\t\t\tPrice: Rs " << bookings[i].p << "\n\t\t\tTickets for this tour=" << bookings[i].tickets << endl;
			cout << "total price of tickets=" << ticket_price << endl;

		}

	}
	if (bookingfound > -1) {
		cout << "\nBooking place" << bookings[bookingfound].place;
		cout << "\nbooking start date" << bookings[bookingfound].sdate;
		cout << "\nbooking end date " << bookings[bookingfound].edate;
		cout << "\nbooking Price" << bookings[bookingfound].p;

	}
	else cout << "\nno match sorry";

}

///==============FUNCTIONS==========///


int main() {

	pkg a, b, c; // places for tour...//
	a.place = "India"; a.sdate = "20, Jan, 2025"; a.edate = "5 Feb, 2025"; a.p = 50000;
	b.place = "Kashmir"; b.sdate = "5, Feb, 2025"; b.edate = "15, Feb, 2025"; b.p = 25000;
	c.place = "Timbaktu"; c.sdate = "15, Feb, 2025"; c.edate = "25, Feb, 2025"; c.p = 80000;

	pkg bookings[100];
	int choice = 0, tkts = 0, ct = 0, choiceagain = 0; // ct is count for booking count//

	// this is only menu ...///
	mydetails();

	cout << "\n";
	packages(a, b, c);														///+++++++         PACKAGES    FUNCTION CALLED           ++++++++///

	while (choice != 5) {
		menu();														///+++++++          MENU   FUNCTION CALLED           ++++++++///
		cin >> choice;
		if (choice == 1) {
			ct = add_bookings(ct, choiceagain, tkts, bookings, a, b, c);

		}



		else if (choice == 2) {
			displaying(ct, bookings);

		}
		else if (choice == 3) {
			ct = cancelling(ct, bookings);


		}


		else if (choice == 4) {
			searching(ct, bookings);

		}

		else if (choice == 5) {
			cout << "Exiting the program...\n";
		}
		else {
			cout << "Invalid choice. Please try again.\n";
		}
	}
	return 0;
}



