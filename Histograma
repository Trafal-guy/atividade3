import javax.imageio.ImageIO;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Created by Marcos on 03/04/2017.
 */
public class Histograma
{
    public static final  String PATH = "C:/Users/Marcos/Documents/Prog 3D/img/gray";

    int[] CalculoHist (BufferedImage img)
    {
        int[] histograma = new int[256];

        for (int y = 0; y < img.getHeight(); y++)
        {
            for (int x = 0; x < img.getWidth(); x++)
            {
                Color cor = new Color(img.getRGB(x, y));
                int r = cor.getRed();
                histograma[r] += 1;
            }
        }
        return histograma;
    }

    public int[] CalculoHistAcum(int[] histograma)
    {
        int[] ha = new int[256];
        ha[0] = histograma[0];
        for (int i = 1; i < histograma.length; i++) {
            ha[i] = histograma[i] + ha[i - 1];
        }
        return ha;
    }

    public int MenorValor (int[] histograma)
    {
        for (int i = 0; i < histograma.length; i++)
        {
            if (histograma[i] != 0)
                return histograma[i];
        }
        return 0;
    }

    public int[] CalculoH (int [] histograma, int pixels)
    {
        int [] h = new int[256];
        int[] ha = CalculoHistAcum(histograma);
        float hmin = MenorValor(histograma);
        for (int i = 0; i < histograma.length; i++)
        {
            h[i] = Math.round(((ha[i] - hmin) / (pixels - hmin)) * 255);
        }
        return h;
    }

    public BufferedImage Equalizacao(BufferedImage img)
    {
        int[] histograma = CalculoHist(img);
        int[] h = CalculoH(histograma, img.getWidth()*img.getHeight());
        BufferedImage out = new BufferedImage(img.getWidth(), img.getHeight(), BufferedImage.TYPE_INT_RGB);
        for (int y = 0; y < img.getHeight(); y++)
        {
            for (int x = 0; x < img.getWidth(); x++)
            {
                Color cor = new Color(img.getRGB(x, y));
                int tom = cor.getRed();
                int novoTom = h[tom];
                Color novaCor = new Color(novoTom, novoTom, novoTom);
                out.setRGB(x, y, novaCor.getRGB());
            }
        }
        return out;
    }

    void run() throws IOException
    {
        BufferedImage img = ImageIO.read(new File(PATH, "car.png"));
        BufferedImage novaImg = Equalizacao(img);
        ImageIO.write(img, "png", new File(PATH, "car2.png"));
    }

    public static void main(String[] args) throws IOException {
        new Histograma().run();
    }

}
