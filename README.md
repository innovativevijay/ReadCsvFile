# ReadCsvFile
This C# code snippet demonstrates a simple CSV file parser that reads data from a specified CSV file, handles cases where values may be enclosed in double quotes, and prints the parsed data to the console. The code utilizes a manual parsing approach, iterating through each line of the CSV file, detecting values within quotes, and constructing a list of string arrays to represent the rows and columns of the CSV data. The code provides a basic understanding of CSV parsing logic in C#.
```sh
void Main()
{
	 // Specify the path of the CSV file
        string filePath = @"C:\Users\Demo\Documents\TestCSV.csv";

        // Create a list to store the data from the CSV file
        List<string[]> data = new List<string[]>();

        try
        {
            // Read all lines from the CSV file
            string[] lines = File.ReadAllLines(filePath);

            foreach (string line in lines)
            {
                List<string> values = new List<string>();
                int startIndex = 0;
                bool withinQuotes = false;

                for (int i = 0; i < line.Length; i++)
                {
                    if (line[i] == '\"')
                    {
                        withinQuotes = !withinQuotes;
                    }
                    else if (line[i] == ',' && !withinQuotes)
                    {
                        string value = line.Substring(startIndex, i - startIndex).Trim('\"');
                        values.Add(value);
                        startIndex = i + 1;
                    }
                }

                string lastValue = line.Substring(startIndex).Trim('\"');
                values.Add(lastValue);

                data.Add(values.ToArray());
            }

            // Print the data from the CSV file
            foreach (string[] row in data)
            {
                foreach (string value in row)
                {
                    Console.Write(value + " ");
                }
                Console.WriteLine();
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
}

// You can define other methods, fields, classes and namespaces here
```
