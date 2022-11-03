#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

bool is_valid(int);			
int rand_num(int, int);
void ask_question(int);
void showStatic(int, int);


int main()
{
	srand(time(0));
	int choice;
	cout << "Welcome to the Math Tutor Program!\n";

	// looping until the user enter '3' to quit
	do
	{
		cout << "\nPlease select from the following menu: \n";
		cout << "1) Addition\n";
		cout << "2) Subtraction\n";
		cout << "3) Quit\n";
		cout << "Enter a choice between 1-3 : ";
		cin >> choice;

		while (is_valid(choice))
		{
			cout << "\nInvalid selection, please choose between 1-3 : ";
			cin >> choice;
		}

		if (choice == 1 || choice == 2)
		{
			ask_question(choice);
		}
		else if (choice == 3)
			cout << "\nThanks for using the Math Tutor Program!\n";

	} while (choice != 3);

	system("pause");
	return 0;
}

// Problem function 
void ask_question(int choice)
{
	int user_low, user_high;
	

	// Ask for the user's range
	cout << "\nWhat range of number would you like to use?\n";
	cout << "Enter low: ";
	cin >> user_low;
	cout << "Enter high: ";
	cin >> user_high;

	int rand_num1 = rand_num(user_low, user_high),
		rand_num2 = rand_num(user_low, user_high);

	int user_answer, correct_answer;



	// Addition question
	if (choice == 1)
	{
		cout << "\nWhat is " << rand_num1 << " + " << rand_num2 << " ? ";
		cin >> user_answer;

		correct_answer = rand_num1 + rand_num2;

		if (user_answer == correct_answer)
		{
			cout << "That's correct!\n";
			
			showStatic(user_answer, correct_answer);
			
		}
		else
		{
			cout << "That's incorrect. The correct answer is " << correct_answer << endl;
			showStatic(user_answer, correct_answer);
		}
	}

	// Subtraction question
	else if (choice == 2)
	{
		cout << "\nWhat is " << rand_num1 << " - " << rand_num2 << " ? ";
		cin >> user_answer;

		correct_answer = rand_num1 - rand_num2;

		if (user_answer == correct_answer)
		{
			cout << "That's correct!\n";
			showStatic(user_answer, correct_answer);
			
		}
		else
		{
			cout << "That's incorrect. The correct answer is " << correct_answer << endl;
			showStatic(user_answer, correct_answer);
		}
	}
}

// Generating random numbers function
int rand_num(int low, int high)
{
	return rand() % (high - low + 1) + low;
}

// Check to see if the input is within the range 1-3
bool is_valid(int choice)
{
	if (choice < 1 || choice > 3)
		return true;
	else
		return false;
}

// Showing accuracy 
void showStatic(int user_answer, int correct_answer)
{
	static float total_question = 0,
		num_right = 0,
		accuracy = 0;
	total_question++;

	if (user_answer == correct_answer)
	{
		num_right++;
		accuracy = (num_right * 100) / total_question;		// Calculate accuracy

		cout << "Your current accuracy is " << accuracy << "% " << endl;
	}
	else
		accuracy = (num_right * 100) / total_question;
}
