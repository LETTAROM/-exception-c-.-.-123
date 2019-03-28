# -exception-c-.-.-123
Свой класс exception c++. Создание собственного класса исключений.  #123
class MyException:public exception//наш класс наследует от базового
{
public:
	MyException(const char *msg,int DataState):exception (msg)//передаем указательна char, чтоб передать какое-н. сообщение
		//вызываем констр-р базового класса и передаем туда эти данные :exception (msg)
	{
		this->DataState = DataState;
	}
	int GetDataState() { return DataState; }//возвращает состояние нашего поля
private:
	int DataState;//хранит состояние инфы, т е что у нас было в переменной, когда вес пошло не так.
	//б.передаваться с исключением

};

void Foo(int value)
{
	if (value < 0)
	{
		throw exception("Число меньше нуля");
	}
	if (value == 1)
	{
		throw MyException("Число равно единице!!!",value); //здесь мы бросим собсвенный класс
	}
	cout << "Переменная= " << value << endl;
}
int main()
{
	setlocale(LC_ALL, "ru");
	try
	{
		Foo(-1);//если сюда бросили целое число, то и ловить ошибку в catch н.
		//с целым числом. Сюда м. передать любое число
		//т е catch (const int ex). Если строку то catch (const char *ex)
	}
	
	catch (MyException& ex)//этот  для нашего класса
	{

		cout << "Блок 1 Мы поймали " << ex.what() << endl;
		cout << "Состояние данных " << ex.GetDataState() << endl;//получили больше инфы что пошло не так с помощью нашего метода
	}
	catch (exception& ex)//этот exception не м поймать наш, т к это разные типы данных
		//но тк наш класс стал наследником от базового, то этот catch поймает и наш класс
		//Блок 1 Мы поймали Unknown exception
	{
		cout << "Блок 2 Мы поймали " << ex.what() << endl;
	}
	//если  2 catch равноценны по передаваемому типу данных, т к наследованы, как эти, то отработает тот catch сто б. идти первым 
	//поэтому более узкоспец-е catch  надо ставить первыми
	return 0;
}
