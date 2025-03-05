Dependency Inversion Principle (DIP) - Principio de Inversión de Dependencias
// Incorrecto: La clase depende directamente de una implementación concreta.
public class EmailService
{
    public void SendEmail(string message) => Console.WriteLine($"Enviando email: {message}");
}

public class Notification
{
    private EmailService _emailService = new EmailService();

    public void NotifyUser()
    {
        _emailService.SendEmail("Tienes una nueva notificación.");
    }
}

// Correcto: Invertir la dependencia mediante una abstracción.
public interface IMessageService
{
    void SendMessage(string message);
}

public class EmailService : IMessageService
{
    public void SendMessage(string message) => Console.WriteLine($"Enviando email: {message}");
}

public class SMSService : IMessageService
{
    public void SendMessage(string message) => Console.WriteLine($"Enviando SMS: {message}");
}

public class Notification
{
    private readonly IMessageService _messageService;

    public Notification(IMessageService messageService)
    {
        _messageService = messageService;
    }

    public void NotifyUser()
    {
        _messageService.SendMessage("Tienes una nueva notificación.");
    }
}
