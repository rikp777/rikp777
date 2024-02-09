``` Java 

import lombok.AllArgsConstructor;
import lombok.Getter;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

@Getter
public class About {
    public static void main(String[] args) {
        About about = new Builder()
                .setName("Rik Peeters")
                .setRole("Software Engineer at Limax")
                .setLanguages(List.of("Java", "Python", "C#", "Typescript"))
                .setTools(List.of("SpringBoot", "NodeJS", "Tailwind", "Vuejs", "Docker", "Neovim"))
                .setArchitectures(List.of("Microservices", "Event-driven", "Design System Pattern"))
                .setGoals(List.of("Contribute to open source projects", "Create my own fitness app to stay motivated and fit"))
                .setPortfolio("https://rikp777.github.io")
                .setCurrentProject("https://rikp777.github.io/RP-Flowcontrol")
                .setExperiences(List.of(
                        new ProfessionalExperience("GoStudent · Freelance", "Aug 2021 - Present", "Tutor in Informatics", "Java, Algoritmen, Python, C++", "https://www.gostudent.org"),
                        new ProfessionalExperience("Limax", "Aug 2018 - Present", "Jr. Software Engineer - Supply Chain / IT", "Vue.js, Microservices, Spring Boot, Java", "https://www.limax.nl"),
                        new ProfessionalExperience("Energy Essentials Group B.V.", "Feb 2022 - Jul 2022", "Software Engineer Intern", ".NET Core, CQRS, C#", "https://www.energyessentials.nl"),
                        new ProfessionalExperience("CytoSMART Technologies B.V.", "Sep 2020 - Feb 2021", "Software Engineer Intern", "Vue.js, .NET Core, C#", "https://cytosmart.com")
                ))
                .build();

        System.out.println(about);
    }

    private final String name;
    private final String role;
    private final List<String> languages;
    private final List<String> tools;
    private final List<String> architectures;
    private final List<String> goals;
    private final String portfolio;
    private final String currentProject;
    private final List<ProfessionalExperience> experiences;

    public About(Builder builder) {
        this.name = builder.name;
        this.role = builder.role;
        this.languages = builder.languages;
        this.tools = builder.tools;
        this.architectures = builder.architectures;
        this.goals = builder.goals;
        this.portfolio = builder.portfolio;
        this.currentProject = builder.currentProject;
        this.experiences = builder.experiences;
    }

    @Override
    public String toString() {
        return AboutFormatter.format(this);
    }

    @Getter
    @AllArgsConstructor
    private static class ProfessionalExperience {
        String company;
        String period;
        String role;
        String skills;
        String url;

        @Override
        public String toString() {
            return AboutFormatter.formatExperience(this);
        }
    }

    private static class AboutFormatter {
        public static String format(About about) {
            return String.format("""
                            👋 Hi there, I'm %s!
                            👨‍💻 Currently, I'm working as %s.
                            💻 I'm proficient in languages such as %s and familiar with tools like %s.
                            🏗️ I enjoy working with architectures like %s.
                            🌱 My future goals include:
                            %s
                            📫 Check out my portfolio at %s for more about my work. Although it might be a bit outdated ✨😅.
                            🔭 I'm currently focusing on my project: %s.             
                            🛠️ I've worked at the following companies:
                                            
                            %s
                            """,
                    about.getName(),
                    about.getRole(),
                    String.join(", ", about.getLanguages()),
                    String.join(", ", about.getTools()),
                    String.join(", ", about.getArchitectures()),
                    formatList(about.getGoals()),
                    about.getPortfolio(),
                    about.getCurrentProject(),
                    formatExperiences(about.getExperiences()));
        }

        private static String formatWithTabs(int tabCount, String text) {
            return "\t".repeat(tabCount) + text;
        }

        private static String formatList(List<String> list) {
            return list.stream()
                    .map(item -> formatWithTabs(1, "• " + item))
                    .collect(Collectors.joining("\n"));
        }

        private static String formatExperiences(List<ProfessionalExperience> experiences) {
            return experiences.stream()
                    .map(AboutFormatter::formatExperience)
                    .collect(Collectors.joining("\n"));
        }

        public static String formatExperience(ProfessionalExperience experience) {
            return String.format("""
                            🏢 %s (%s)
                            🔨 %s
                            🛠️ %s
                            🌐 %s
                            """,
                    experience.getCompany(),
                    experience.getPeriod(),
                    formatWithTabs(2, "Role: " + experience.getRole()),
                    formatWithTabs(2, "Skills: " + experience.getSkills()),
                    formatWithTabs(2, "More info: " + experience.getUrl()));
        }
    }

    public static class Builder {
        private String name;
        private String role;
        private List<String> languages;
        private List<String> tools;
        private List<String> architectures;
        private List<String> goals;
        private String portfolio;
        private String currentProject;
        private List<ProfessionalExperience> experiences;

        public Builder setName(String name) {
            if (name == null || name.trim().isEmpty())
                throw new IllegalArgumentException("Attempting to be anonymous? Please provide a name.");
            this.name = name;
            return this;
        }

        public Builder setRole(String role) {
            if (role == null || role.trim().isEmpty())
                throw new IllegalArgumentException("Everyone has a role in this world, even you. Don't leave it blank.");
            this.role = role;
            return this;
        }

        public Builder setLanguages(List<String> languages) {
            if (languages == null || languages.isEmpty())
                throw new IllegalArgumentException("Silence is golden, but not when it comes to programming languages. Add some!");
            this.languages = new ArrayList<>(languages); // Defensive copying
            return this;
        }

        public Builder setTools(List<String> tools) {
            if (tools == null || tools.isEmpty())
                throw new IllegalArgumentException("Without tools, we're just making sandcastles. Please specify some tools.");
            this.tools = new ArrayList<>(tools);
            return this;
        }

        public Builder setArchitectures(List<String> architectures) {
            if (architectures == null || architectures.isEmpty())
                throw new IllegalArgumentException("Even architects in ancient times had plans. What's yours?");
            this.architectures = new ArrayList<>(architectures);
            return this;
        }

        public Builder setGoals(List<String> goals) {
            if (goals == null || goals.isEmpty())
                throw new IllegalArgumentException("Without any goals, you won't get far in life. Please add some!");
            if (goals.size() < 2)
                throw new IllegalArgumentException("Without some goals, you won't get far in life. Please add some more!");

            this.goals = new ArrayList<>(goals);
            return this;
        }

        public Builder setPortfolio(String portfolio) {
            if (portfolio == null || portfolio.trim().isEmpty())
                throw new IllegalArgumentException("A portfolio is worth a thousand lines of code. Don't leave it out.");

            this.portfolio = portfolio;
            return this;
        }

        public Builder setCurrentProject(String currentProject) {
            if (currentProject == null || currentProject.trim().isEmpty())
                throw new IllegalArgumentException("No current project? Are you in stealth mode? Please share!");

            this.currentProject = currentProject;
            return this;
        }

        public Builder setExperiences(List<ProfessionalExperience> experiences) {
            if (experiences == null || experiences.isEmpty())
                throw new IllegalArgumentException("Experience is the teacher of all things. Surely, you've learned something?");

            this.experiences = new ArrayList<>(experiences);
            return this;
        }

        public About build() {
            validateState();
            return new About(this);
        }

        private String validateString(String input, String errorMessage) {
            if (input == null || input.trim().isEmpty()) {
                throw new IllegalArgumentException(errorMessage);
            }
            return input;
        }

        private void validateState() {
            if (name == null || role == null || languages == null || tools == null ||
                    architectures == null || goals == null || portfolio == null ||
                    currentProject == null || experiences == null) {
                throw new IllegalStateException("""
                        Seems like we're missing some chapters of your story.
                        Don't leave us hanging; fill in all the details to complete the narrative!
                        """);
            }
        }
    }
}
```
