import java.io.BufferedReader;

import java.io.IOException;

import java.io.InputStreamReader;


public interface test
{

	void doCalculation();
	void getResult();

}


class Calculate implements test
{

	private char op;
	
	private int resultcal;
	
	private double resultsin;
	
	private int first,second;
	
	private boolean checki,checkd;
	
	private double num;
	
	Calculate()
	{	
	
	}
	Calculate(Double dblNum,char cOperator)
	{
		num = dblNum;
		op = cOperator;
		checkd = true;
	}
	public Calculate(int iFirstNum, char cOperator, int iSecondNum)
	{
		first = iFirstNum;
		op = cOperator;
		second = iSecondNum;
		checki=true;
	}
	public void doCalculation() 
	{
		switch(op)
		{
			case '+':
				checkInt();
				resultcal = first + second;
				break;
			case '-':
				checkInt();
				resultcal = first - second;
				break;
			case '*':
				checkInt();
				resultcal = (first * second);
				break;
			case '/':
				checkInt();
				checkSecondNum();
				resultcal = (first / second);
				break;
			case 's' :
			case 'S':
				checkDouble();
				resultsin = Math.sin(Math.toRadians(num));
				break;
			case 'c':
			case 'C':
				checkDouble();
				resultsin = Math.cos(Math.toRadians(num));
				break;
			case 't' :
			case 'T':
				checkDouble();
				resultsin = Math.tan(Math.toRadians(num));
				break;
			case 'l':
			case 'L':
				checkDouble();
				resultsin = Math.log(num);
				break;
			default:
				System.out.println("Invalid input!!!!!");
				break;
			
		}
	}

	public void getResult() {
		if(checki)
		{
			System.out.println("The result is : " + resultcal);
		}
		else if(checkd)
		{
			System.out.println("The result is : " + resultsin);
		}
	}
	public void checkSecondNum()
	{
		if(second == 0)
		{
			System.out.println("Division cannot be performed as denominator is zero");
			System.exit(0);
		}
		else
		{
			System.out.println("The numbers can be divided.");
		}
	}
	public void checkInt()
	{
		if(checki)
		{
			System.out.println("Calculating using Calculator!!!");
		}
		else
		{
			System.out.println("Errorr!!");
			System.exit(0);
		}
	}
	public void checkDouble()
	{
		if(checkd)
		{
			System.out.println("Calculating using Scitific Calculator!!!");
		}
		else
		{
			System.out.println("Errorr!!");
			System.exit(0);
		}
	}
	
}

class Calculator {

	public void Calculation() throws IOException
	{
		boolean next = true;
		do
		{
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
			int firstnum = 0,secondnum=0;
			System.out.println("Enter first number : ");
			try
			{
				firstnum = Integer.parseInt(br.readLine());
			}
			catch(NumberFormatException e)
			{
				System.out.println("Enter a number only as input!!!!! "+e);
				System.exit(0);
			}
			System.out.println("Enter any one operator (+,-,*,/)");
			String op = br.readLine();
			char operator = op.charAt(0);
			if(operator == '+' || operator == '-' || operator == '*' || operator == '/')
			{
				System.out.println("Enter second number : ");
				try 
				{
					secondnum = Integer.parseInt(br.readLine());
				} 
				catch (NumberFormatException e) 
				{
					System.out.println("Enter a number only as input!!!!! "+e);
					System.exit(0);
				}
				Calculate cal = new Calculate(firstnum,operator,secondnum);
				cal.doCalculation();
				cal.getResult();
				System.out.println("Do you want to continue the calculation (1/0)?");
				int in = Integer.parseInt( br.readLine());
				if(in == 1)
				{
						next=true;
				}
				else if(in == 0)
				{
					next=false;
					System.out.println("Thank you!!!");
				}
				else
				{
					System.out.println("Invalid input. Enter 1/0");
				}
			}
				
			else
			{
				System.out.println("Invalid!!!! Enter only above mentioned 4 operators!!! ");
				System.exit(0);
			}
			
		}while(next);
	}
	
}


class ScientificCalculator extends Calculate
{
	
	double number=0;
	char operator = 0;
	
	void ScientificCalculation() throws IOException
	{
		boolean next=true;
		do
		{
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
			System.out.println("Enter the number to perform operation : ");
			try 
			{
				number = Double.parseDouble(br.readLine());
			} 
			catch (NumberFormatException e) 
			{
				System.out.println("Invalid!!! Enter only Numbers!!!! " + e);
				System.exit(0);
			} 
			System.out.println("Enter the operator as : sine/cosine/tangent/log");
			String operator1 = br.readLine();
			char operator = operator1.charAt(0);
			if( operator =='s' || operator=='c' || operator=='t' || operator=='l' )
			{
				Calculate scal = new Calculate(number,operator);
				scal.doCalculation();
				scal.getResult();
				System.out.println("Do you want to continue the calculation (1/0)?");
				int check = Integer.parseInt(br.readLine());
				if(check == 1)
				{
					next=true;
				}
				else if(check == 0)
				{
					next = false;
					System.out.println("Thank you!!!");
				}
				else
				{
					System.out.println("Enter only 1 or 0!!!");
				}
				
			}
			else
			{
				System.out.println("Enter only the 4 operations mentioned above!!!");
				System.exit(0);
			}
		}while(next);
	}


}


class UseCalculate {
	
	public static void main(String[] args) throws IOException {
			boolean next = true;
			do
			{
				System.out.println("What type of operations do you want to perform:");
				System.out.println("1.Basic");
				System.out.println("2.Scientific");
				BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
				int choice = Integer.parseInt(br.readLine());
				switch(choice)
				{
				case 1:
					Calculator obj = new Calculator();
					obj.Calculation();
					break;
				case 2:
					ScientificCalculator obj2 = new ScientificCalculator();
					obj2.ScientificCalculation();
					break;
				}
				System.out.println("Do you want to continue to use the calculator (1/0)? ");
				int check = Integer.parseInt(br.readLine());
				if(check == 1)
				{
					next = true;
				}
				else if (check == 0)
				{
					next = false;
					System.out.println("Thank you!!!");
				}
				else
				{
					System.out.println("Invalid input please enter 1 or 0");
					System.exit(0);
				}
			}while(next);
		}

}
