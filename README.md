DevOps CI/CD-Pipeline
Erstellen ein neues Projekt Nutzen von Github, Jenkins, SonarQube und Docker.

![image001](https://github.com/user-attachments/assets/46c40903-25a6-4454-8521-b3eac693ce1a)


Kurze Projektbeschreibung:
Ich möchte mein neues Projekt vorstellen, bei dem meine Website auf einem Docker-Server bereitgestellt wird. Die verwendeten Ressourcen für dieses Projekt sind:

VSCode, um mein Repository von GitHub zu klonen

GitHub-Webhooks für automatische Trigger

AWS-Instanzen für die Server:

Jenkins zur Automatisierung der Pipeline

SonarQube zur Überprüfung des Codes auf Sicherheitslücken

Docker zur Bereitstellung der Website

Um einen sicheren Zugriff auf die Website über den Browser zu ermöglichen, habe ich ein SSL-Zertifikat im AWS Certificate Manager erstellt und einen CNAME-Eintrag in AWS Route 53 eingerichtet. Außerdem habe ich eine CloudFront-Distribution mit einem A-Eintrag erstellt, um den Datenverkehr an meinen Docker-Server mit installierter Nginx-Anwendung weiterzuleiten.

Dieses Projekt ist eine CI/CD-Pipeline, die meine Website mithilfe einer automatisierten Pipeline in Docker ausführt und den Zugriff über HTTPS ermöglicht.

📌 Schritte zur Umsetzung
1-Ich habe drei Ubuntu T2.medium Instanzen auf AWS erstellt für:

  • Jenkins-Server

  • SonarQube-Server

  • Docker-Server ↓
![image](https://github.com/user-attachments/assets/37c808b8-6922-4603-b14e-3e09aa72d742)

2-Ich habe mich über das Terminal mit den Servern verbunden und deren Hostnamen entsprechend angepasst mit Commando hostnamectl set-hostname <Server Name>. ↓
![image](https://github.com/user-attachments/assets/4593f761-d9d7-4bc8-a007-3716e6545354)

3-In GitHub habe ich ein Repository erstellt und mit VSCode mein Repository geklont.
  Dort habe ich HTML- und CSS-Dateien sowie eine Dockerfile geschrieben und alles in das Repository gepusht:
  👉 GitHub Repository – website-jenkins-docker

4-Ich habe in GitHub Webhooks eingerichtet, um automatisch Änderungen im Repository über die Jenkins-Pipeline zu triggern.

5-Ich habe auf meinen Jenkins-Server über den Browser zugegriffen, die benötigten Plugins wie Docker und SonarScanner installiert und anschließend eine Pipeline erstellt, die automatisch auf Änderungen im GitHub-Repository reagiert.

6-In SonarQube habe ich ein Projekt mit dem Namen website-jenkins-docker erstellt.
  Nach dem Erstellen eines Tokens für Jenkins habe ich die IP-Adresse und den Token des SonarQube-Servers in Jenkins integriert. ↓↓
  ![image](https://github.com/user-attachments/assets/dcbd004e-7010-4836-8e9e-98fafc20606d)
  ![image](https://github.com/user-attachments/assets/486d6296-83d3-4706-9ab1-fa873fee76ab)

7-Nach einer erfolgreichen Analyse durch SonarQube habe ich den Docker-Server in die Jenkins-Pipeline integriert.
  Über den SSH-Agent wurde das Projekt website-jenkins-docker auf dem Docker-Server ausgeführt, und Nginx wurde dort installiert.

8-Ich konnte meine Website im Browser über localhost und den HTTP-Port aufrufen. ↓
  ![image](https://github.com/user-attachments/assets/ee4382f3-51ea-45e6-ba04-381d65adf6e3)

9-Für eine sichere HTTPS-Verbindung (Port 443) habe ich:

  •Ein SSL-Zertifikat im AWS Certificate Manager (ACM) erstellt

  •Einen CNAME-Eintrag in AWS Route 53 gesetzt ↓
   ![image](https://github.com/user-attachments/assets/2d5433d9-06a9-4b85-80c6-0481961cb2fe)

10-Zur Weiterleitung des Traffics habe ich eine CloudFront-Distribution erstellt,
die das bereits in ACM generierte SSL-Zertifikat verwendet.
Mit einem A-Eintrag in Route 53 wird der Traffic von Port 80 (HTTP) auf Port 443 (HTTPS) zum Docker-Server geleitet, der die Website hostet. ↓
![image](https://github.com/user-attachments/assets/ea13e3e9-ef47-4196-a309-3e683e8fd3e5)

Am Ende konnte ich erfolgreich auf meine Website über eine sichere HTTPS-Verbindung (Port 443)
unter meiner persönlichen Domain mahmoodi-tech.de zugreifen: ↓
![image](https://github.com/user-attachments/assets/4401a348-19eb-4d39-99fb-b077a7bb4fbc)



✅ Ergebnis
Eine vollständige CI/CD-Pipeline, die:

Änderungen automatisch von GitHub abruft

Den Code auf Schwachstellen mit SonarQube überprüft

Die Website auf einem Docker-Server bereitstellt

Über HTTPS sicher zugänglich ist






