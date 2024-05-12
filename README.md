import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.Random;

public class RandomPictureSelector {

    public static void main(String[] args) {
        String url = "https://www.flickr.com/search/?text=tractor";
        String randomPictureUrl = getRandomPicture(url);
        System.out.println("Random Picture Source: " + randomPictureUrl);
    }

    public static String getRandomPicture(String url) {
        try {
            // Fetch the HTML content of the webpage
            Document doc = Jsoup.connect(url).get();

            // Extract image sources from img tags
            Elements imgTags = doc.select("img");
            List<String> imageSources = new ArrayList<>();
            for (Element img : imgTags) {
                String src = img.attr("src");
                if (!src.isEmpty()) {
                    imageSources.add(src);
                }
            }

            // Select a random image source
            Random random = new Random();
            String randomImageSource = imageSources.get(random.nextInt(imageSources.size()));

            return randomImageSource;
        } catch (IOException e) {
            System.out.println("Error: Failed to fetch URL: " + url);
            e.printStackTrace();
            return null;
        }
    }
}
