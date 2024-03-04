#include <iostream>
#include <string>
#include <cstring>
#include <Windows.h>
#include <time.h>
#include <conio.h>

#define R_KEY 82
#define r_key 114
#define _0exit 48
std::string taskstr = "`1234567890-=~!@#$%^&*()_+qwertyuiop[]asdfghjkl;'zxcvbnm,./QWERTYUIOP{}|ASDFGHJKL:ZXCVBNM<>?";

void toClipboard(HWND hwnd, const std::string& s) {
	OpenClipboard(hwnd);
	EmptyClipboard();
	HGLOBAL hg = GlobalAlloc(GMEM_MOVEABLE, s.size() + 1);
	if (!hg) {
		CloseClipboard();
		return;
	}
	memcpy(GlobalLock(hg), s.c_str(), s.size() + 1); // я хз поч жалуется, оно никогда не будет 0
	GlobalUnlock(hg);
	SetClipboardData(CF_TEXT, hg);
	CloseClipboard();
	GlobalFree(hg);
}

std::string chargen(int limit)
{
	std::string generator;
	for (int i = 1; i < 1 + limit + 10; i++)
	{
		char x = taskstr[rand() % 93];
		generator += x;
	}
	return generator;
}
std::string regen(int limit, int gen)
{
	std::string keep;
	for (int i = 0; i < gen; i++)
	{
		chargen(limit);
		if (i == gen - 1)
		{
			keep = chargen(limit);
		}
	}
	return keep;
}
// chargen и regen являются функциями для рандомайзера символов
std::string Randomize()
{
	time_t currentTime{}; // в коде создаётся переменная, хранящая все данные про текущее время
	time(&currentTime); // вот, ток тут не в числовом формате
	struct tm* myTime = localtime(&currentTime); // теперь создаётся int переменная, в которой хранятся данные о времени в числовом формате
	int limit = myTime->tm_hour + 10;
	int gen = myTime->tm_sec;
	std::string str = regen(limit, gen);
	return str.c_str();
}
void GenerateAndCopy()
{
	HWND hwnd = GetDesktopWindow();
	std::string string = Randomize();
	std::cout << "Your random string: " << string << "\n";
	toClipboard(hwnd, string);
	std::cout << "Copied to clipboard\n";
}
int main()
{
	int input = 0;
	std::cout << "Enter r to generate a random string.\nEnter 0 to terminate program\n";
	while (1)
	{
		switch (input = _getch())
		{
		case _0exit:
			return 0;
		case R_KEY:
		case r_key:
			GenerateAndCopy();
		default:
			break;
		}
	}
}
