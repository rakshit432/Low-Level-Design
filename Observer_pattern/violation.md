```mermaid
classDiagram

class YoutubeChannel {
    +upload(video)
    +sendEmail(video)
    +sendSMS(video)
    +sendPush(video)

    Problems:
    Tight Coupling
    Violates SRP
    Violates OCP
}

class Main {
    +main()
}

Main ..> YoutubeChannel : creates
```