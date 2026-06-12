```mermaid
classDiagram

class YoutubeChannel {
    +upload(video)
    +sendEmail(video)
    +sendSMS(video)
    +sendPush(video)
}

class Main {
    +main()
}

Main ..> YoutubeChannel : creates

note for YoutubeChannel
  Problems:
  - Tight Coupling
  - Violates SRP
  - Violates OCP

  New Notification:
  WhatsApp/Slack

  => Modify YoutubeChannel
end note
```