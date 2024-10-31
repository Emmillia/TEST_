# TEST_
Куценок Эмилия Сергеевна
Задание 2 
package currencyconverter;

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Введите сумму в USD для конвертации: ");

        // Проверка на ввод корректного числа
        if (scanner.hasNextDouble()) {
            double amountInUSD = scanner.nextDouble();
            if (amountInUSD < 0) {
                System.out.println("Сумма не может быть отрицательной.");
            } else {
                CurrencyConverter.convertCurrency(amountInUSD);
            }
        } else {
            System.out.println("Пожалуйста, введите корректное число.");
        }

        scanner.close();
    }
}
package currencyconverter;

public class CurrencyConverter {
    // Обменные курсы (константы)
    private static final double USD_TO_EUR = 0.91937;
    private static final double USD_TO_GBP = 0.77071;
    private static final double USD_TO_JPY = 152.74;
    private static final double USD_TO_INR = 84.08;
    private static final double USD_TO_AUD = 1.52;

    public static void convertCurrency(double amountInUSD) {
        System.out.printf("Сумма в USD: %.2f%n", amountInUSD);
        System.out.printf("Сумма в EUR: %.2f%n", amountInUSD * USD_TO_EUR);
        System.out.printf("Сумма в GBP: %.2f%n", amountInUSD * USD_TO_GBP);
        System.out.printf("Сумма в JPY: %.2f%n", amountInUSD * USD_TO_JPY);
        System.out.printf("Сумма в INR: %.2f%n", amountInUSD * USD_TO_INR);
        System.out.printf("Сумма в AUD: %.2f%n", amountInUSD * USD_TO_AUD);
    }
}

Задание 3

package simplepasswordgenerator;

import java.util.InputMismatchException;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int length = 0;

        while (true) {
            System.out.print("Введите длину пароля (от 8 до 12 символов): ");
            try {
                length = scanner.nextInt();
                // Проверка на допустимую длину пароля
                if (length >= 8 && length <= 12) {
                    break;
                } else {
                    System.out.println("Ошибка: длина пароля должна быть от 8 до 12 символов.");
                }
            } catch (InputMismatchException e) {
                System.out.println("Ошибка: введите целое число.");
                scanner.next();
            }
        }

        String password = SimplePasswordGenerator.generatePassword(length);
        System.out.println("Сгенерированный пароль: " + password);
        scanner.close();
    }
}
package simplepasswordgenerator;

import java.security.SecureRandom;

public class SimplePasswordGenerator {
    private static final String UPPERCASE = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    private static final String LOWERCASE = "abcdefghijklmnopqrstuvwxyz";
    private static final String DIGITS = "0123456789";
    private static final String SPECIAL_CHARS = "!@#$%^&*()-_=+<>?";
    private static final String ALL_CHARS = UPPERCASE + LOWERCASE + DIGITS + SPECIAL_CHARS;

    public static String generatePassword(int length) {
        SecureRandom random = new SecureRandom();
        StringBuilder password = new StringBuilder(length);

        // Гарантируем наличие хотя бы одной буквы верхнего регистра, одной нижнего регистра,
        // одной цифры и одного специального символа
        password.append(UPPERCASE.charAt(random.nextInt(UPPERCASE.length())));
        password.append(LOWERCASE.charAt(random.nextInt(LOWERCASE.length())));
        password.append(DIGITS.charAt(random.nextInt(DIGITS.length())));
        password.append(SPECIAL_CHARS.charAt(random.nextInt(SPECIAL_CHARS.length())));

        // Заполняем оставшуюся часть пароля случайными символами
        for (int i = 4; i < length; i++) {
            password.append(ALL_CHARS.charAt(random.nextInt(ALL_CHARS.length())));
        }

        return shuffleString(password.toString());
    }

    private static String shuffleString(String input) {
        char[] characters = input.toCharArray();
        SecureRandom random = new SecureRandom();
        for (int i = characters.length - 1; i > 0; i--) {
            int j = random.nextInt(i + 1);
            char temp = characters[i];
            characters[i] = characters[j];
            characters[j] = temp;
        }
        return new String(characters);
    }
}
