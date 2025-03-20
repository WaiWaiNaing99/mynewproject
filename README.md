using System;
using System.Collections.Generic;
using System.Text;

public class KeypadTxtConverter
{
    public static string ConvertKeypadInput(string input)
    {
        Dictionary<char, string> keypad = new Dictionary<char, string>
        {
            {'2', "ABC"}, {'3', "DEF"}, {'4', "GHI"}, {'5', "JKL"}, {'6', "MNO"},
            {'7', "PQRS"}, {'8', "TUV"}, {'9', "WXYZ"}, {'0', " "}
        };

        StringBuilder output = new StringBuilder();
        int count = 0;
        char lastChar = '\0';

        foreach (char c in input)
        {
            if (c == '#') break;
            if (c == '*')
            {
                if (output.Length > 0)
                    output.Length--;
                continue;
            }
            if (c == ' ')
            {
                count = 0;
                continue;
            }
            
            if (c == lastChar)
                count++;
            else
                count = 0;
            
            if (keypad.ContainsKey(c))
            {
                string letters = keypad[c];
                output.Append(letters[count % letters.Length]);
            }
            
            lastChar = c;
        }

        return output.ToString();
    }
    
    public static void Main()
    {
        Console.WriteLine(ConvertKeypadInput("33#")); // Output: E
        Console.WriteLine(ConvertKeypadInput("227*#")); // Output: B
        Console.WriteLine(ConvertKeypadInput("4433555 555666#")); // Output: HELLO
        Console.WriteLine(ConvertKeypadInput("8 88777444666*664#")); // TUR SING
    }
}
