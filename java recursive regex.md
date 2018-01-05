## Unit test
```java
import com.google.common.io.Resources;
import org.junit.Test;

import java.io.IOException;
import java.net.URL;
import java.nio.charset.Charset;

import static org.assertj.core.api.Assertions.assertThat;

public class HtmlParserTest {

    @Test
    public void canDeactivateComplexHtmlContent() throws IOException {
        URL resource = Resources.getResource("index.html");
        String content = Resources.toString(resource, Charset.defaultCharset());

        String result = new HtmlParser(content).deactivateLinks();

        assertThat(result).doesNotContain("<a href");
        assertThat(result).doesNotContain("</a>");
    }

    @Test
    public void canDeactivateSimpleText() throws IOException {
        String content = "<div><a href=\"link\">link</a></div>";

        String result = new HtmlParser(content).deactivateLinks();

        assertThat(result).doesNotContain("<a href");
        assertThat(result).doesNotContain("</a>");
    }
}
```

## Class
```java
import com.google.gwt.regexp.shared.MatchResult;
import com.google.gwt.regexp.shared.RegExp;

public class HtmlParser {

    //https://regex101.com/r/Bg9xUt/2

    private static final String HREF_REGEX = "(<a.*?\">(\\D.*|\\D*)<\\/a>)";
    private final RegExp compile = RegExp.compile(HREF_REGEX);
    private String content;

    public HtmlParser(final String content) {
        this.content = content;
    }


    public String deactivateLinks() {
        return apply(content);
    }

    protected String apply(String content) {
        MatchResult matchResult = compile.exec(content);
        if(matchResult != null) {
            content = apply(content.replace(matchResult.getGroup(0), matchResult.getGroup(2)));
        }
        return content;
    }
}
```
