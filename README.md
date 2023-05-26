namespace RikPeeters
{
    class About extends Me
    {
        public string Name => "Rik Peeters";
        public string Role => "Software Engineer at Limax";
        public string[] Languages => new string[] { "PHP", "Javascript", "Java", "Python", "C#" };
        public string[] Tools => new string[] { "SpringBoot", "Laravel", "Node", "Tailwind", "Vuejs", "Nuxtjs", "Docker", "Neovim" };
        public string[] Architectures => new string[] { "Microservices", "Event-driven", "Design System Pattern" };
        public string[] Goals => new string[] { "Contribute to open source projects", "Create my own fitness app to stay motivated and fit" };
        public string Portfolio => "rikp777.github.io";
        public string CurrentProject => "rikp777.github.io/RP-Flowcontrol";

        public override string ToString()
        {
            return $"👋 Hi there, I'm {Name}!\n" +
                   $"👨‍💻 Currently, I'm working as {Role}.\n" +
                   $"💻 I'm proficient in {string.Join(", ", Languages)} and familiar with tools like {string.Join(", ", Tools)}.\n" +
                   $"🏗️ I enjoy working with {string.Join(", ", Architectures)} architectures.\n" +
                   $"🌱 My future goals are {string.Join(" and ", Goals)}.\n" +
                   $"📫 You can see more of my work on my portfolio: {Portfolio}.\n" +
                   $"🔭 I'm currently working on my project: {CurrentProject}.";
        }
    }
}
