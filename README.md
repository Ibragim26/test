import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.LinkedHashSet;
import java.util.Objects;
import java.util.Scanner;
import java.util.Set;

public class App {
    public static void main(String[] args) {

        String flag = "y";
        while (Objects.equals(flag, "y")) {
            System.out.println("Вы хотите запустить программу? (y/n)");
            Scanner scanner = new Scanner(System.in);
            flag = scanner.nextLine();
            if (Objects.equals(flag, "y")) {
                System.out.println("Пожалуйста, укажите имя текстового файла.");
                String fileName = scanner.nextLine();
                printUniqueChars(fileName);
                System.out.println();
            } else {
                flag = "n";
            }
        }
    }

    public static void printUniqueChars(String fileName) {
        try (BufferedReader reader = new BufferedReader(new FileReader(fileName))){
            String line;
            Set<Character> uniqueCharacters = new LinkedHashSet<>();
            while ((line = reader.readLine()) != null) {
                String[] words = line.split("\\s+");
                for (String word : words) {
                    for (char c : word.toCharArray()) {
                        uniqueCharacters.add(c);
                    }
                }
            }
            
            Character last = uniqueCharacters.stream().reduce((first, second) -> second).get();

            for (Character c : uniqueCharacters) {
                System.out.print(c);
                if(!c.equals(last)) {
                    System.out.print(", ");
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}



