``` Java 
import java.util.List;

public class About {

    private final String name;
    private final String role;
    private final List<String> languages;
    private final List<String> tools;
    private final List<String> architectures;
    private final List<String> goals;
    private final String portfolio;
    private final String currentProject;

    public About() {
        this.name = "Rik Peeters";
        this.role = "Software Engineer at Limax";
        this.languages = List.of("Java", "Python", "C#", "Typescript");
        this.tools = List.of("SpringBoot", "NodeJS", "Tailwind", "Vuejs", "Docker", "Neovim");
        this.architectures = List.of("Microservices", "Event-driven", "Design System Pattern");
        this.goals = List.of("Contribute to open source projects", "Create my own fitness app to stay motivated and fit");
        this.portfolio = "rikp777.github.io";
        this.currentProject = "rikp777.github.io/RP-Flowcontrol";
    }
  
    @Override
    public String toString() {
        return """
            👋 Hi there, I'm %s!
            👨‍💻 Currently, I'm working as %s.
            💻 I'm proficient in %s and familiar with tools like %s.
            🏗️ I enjoy working with %s architectures.
            🌱 My future goals are %s.
            📫 You can see more of my work on my portfolio: %s.
            🔭 I'm currently working on my project: %s.
            """.formatted(
                name,
                role,
                String.join(", ", languages),
                String.join(", ", tools),
                String.join(", ", architectures),
                String.join(", ", goals),
                portfolio,
                currentProject);
    }

    public static void main(String[] args){
        About about = new About();
        System.out.println(about);
    }
}
```
