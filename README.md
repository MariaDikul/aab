## Описание

Есть программу, которая генерирует **25** строк размером **30 000** символов, которые состоят из символов **'a'** и **'b'**. Для каждой строки необходимо найти размер наибольшего промежутка, состоящего из одних символов 'a'. Например, для строки "aaababbaaaaabaa" ответом будет число 5 — 5 символов 'a' подряд. 

Нужно скопировать код программы и запустить. Программа окажется слишком медленной, **задача — ускорить её средствами многопоточного программирования**. А затем модифицируйте код программы так, чтобы можно было найти максимальный интервал значений среди всех строк.

**Менять этот алгоритм вам нельзя.**

КОД:

```java
import java.util.*;

public class Main {

    public static void main(String[] args) throws InterruptedException {
        String[] texts = new String[25];
        for (int i = 0; i < texts.length; i++) {
            texts[i] = generateText("aab", 30_000);
        }

        long startTs = System.currentTimeMillis(); // start time
        for (String text : texts) {
            int maxSize = 0;
            for (int i = 0; i < text.length(); i++) {
                for (int j = 0; j < text.length(); j++) {
                    if (i >= j) {
                        continue;
                    }
                    boolean bFound = false;
                    for (int k = i; k < j; k++) {
                        if (text.charAt(k) == 'b') {
                            bFound = true;
                            break;
                        }
                    }
                    if (!bFound && maxSize < j - i) {
                        maxSize = j - i;
                    }
                }
            }
            System.out.println(text.substring(0, 100) + " -> " + maxSize);
        }
        long endTs = System.currentTimeMillis(); // end time

        System.out.println("Time: " + (endTs - startTs) + "ms");
    }

    public static String generateText(String letters, int length) {
        Random random = new Random();
        StringBuilder text = new StringBuilder();
        for (int i = 0; i < length; i++) {
            text.append(letters.charAt(random.nextInt(letters.length())));
        }
        return text.toString();
    }
}
```

## Решение
https://github.com/MariaDikul/aab/blob/max/src/main/java/ru/netology/Main.java
