import java.io.File;
import java.io.FileNotFoundException;
import java.util.*;

public class CompareFile {
    static float compareStr(String s1, String s2)
    {
        int i=0;
        int l;
        float avg;
        int count=0;
        if(s1.length()<s2.length()) {

                StringTokenizer tokenizer1 = new StringTokenizer(s1);
                StringTokenizer tokenizer2 = new StringTokenizer(s2);

            Map<String, Integer> map = new HashMap<>();

                while (tokenizer2.hasMoreTokens()) {
                    String word = tokenizer2.nextToken();
                     map.put(word,i);
                     i++;

                }
                l=i;
            while (tokenizer1.hasMoreTokens()){
                String word = tokenizer1.nextToken();

                if(map.get(word)!=null)
                    count++;

            }
            avg=((float)count/(float)l)*100;

        }
        else {

            StringTokenizer tokenizer1 = new StringTokenizer(s1);
            StringTokenizer tokenizer2 = new StringTokenizer(s2);
            Map<String, Integer> map = new HashMap<>();

            while (tokenizer1.hasMoreTokens()) {
                String word = tokenizer1.nextToken();
                map.put(word,i);
                i++;
            }
            l=i;
            while (tokenizer2.hasMoreTokens()){
                String word = tokenizer2.nextToken();
                if(map.get(word)!=null)
                    count++;
            }
             avg=((float)count/(float)l)*100;
        }
        return avg;
    }
    public static void main(String[] args) {
        // Specify the path to your Word file
        String filePath1 = "C:\\Users\\priya\\OneDrive\\Documents\\Cheating1.txt";
        String filePath2 = "C:\\Users\\priya\\OneDrive\\Documents\\CheatingParaphrased.txt";
        try {
            File file = new File(filePath1);
            Scanner scanner1 = new Scanner(file);
            scanner1.useDelimiter("\\.");
            File file2 = new File(filePath2);
            Scanner scanner2 = new Scanner(file2);
            scanner2.useDelimiter("\\.");
            Map<Integer,String> hashMap1 = new HashMap<>();
            Map< Integer,String> hashMap2 = new HashMap<>();
            // Read the content line by line
            int i=0;
            while (scanner1.hasNextLine()) {

                String line1 = scanner1.next();
                hashMap1.put(i,line1);
                i++;
            }
             i=0;
            while (scanner2.hasNextLine()) {

                String line1 = scanner2.next();
                hashMap2.put(i,line1);
                i++;
            }
            int c=0;
            float ans=0;
            int j=0;
            i=0;
            Iterator<Map.Entry< Integer,String>> iterator1 = hashMap1.entrySet().iterator();
            System.out.println("The sentences similar in both the files are : ");
            System.out.println();
            while (iterator1.hasNext()) {

                String s1= String.valueOf(hashMap1.get(i));
                j=0;
                Iterator<Map.Entry< Integer,String>> iterator2 = hashMap2.entrySet().iterator();
                while(iterator2.hasNext())
                {

                    String s2= String.valueOf(hashMap2.get(j));
                    float same=compareStr(s1,s2);
                    ans=ans+same;
                    if(same>=70.0) {
                        System.out.println(s1);
                        c++;
                    }
                    j++;
                    Map.Entry<Integer, String> entry = iterator2.next();
                }
                i++;
                Map.Entry<Integer, String> entry = iterator1.next();
            }
            System.out.println();
            System.out.println("Percentage Similarity of the two file :" +((float)c/(float)(i))*100);
            scanner1.close();
            scanner2.close();
        } catch (FileNotFoundException e) {
            System.out.println("File not found ");
        }
    }
}
