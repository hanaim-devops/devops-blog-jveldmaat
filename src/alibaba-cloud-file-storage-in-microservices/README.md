# Alibaba Cloud File Storage in Microservices

<img src="plaatjes/alibaba_logo.png" width="250" align="right" alt="mdbook logo om weg te halen" title="Alibaba Cloud Logo">

_[Jesse Veldmaat, oktober 2024.](https://github.com/hanaim-devops/blog-student-naam)_

<hr/>

## Inhoudsopgave

- [Alibaba Cloud File Storage in Microservices](#alibaba-cloud-file-storage-in-microservices)
  - [Inhoudsopgave](#inhoudsopgave)
  - [Het toepassen van Alibaba Cloud File Storage in een self-managed microservices-architectuur](#het-toepassen-van-alibaba-cloud-file-storage-in-een-self-managed-microservices-architectuur)
    - [Wat zijn de belangrijkste kenmerken en mogelijkheden van Alibaba Cloud File Storage?](#wat-zijn-de-belangrijkste-kenmerken-en-mogelijkheden-van-alibaba-cloud-file-storage)
    - [Welke voordelen biedt Alibaba Cloud File Storage ten opzichte van traditionele file storage?](#welke-voordelen-biedt-alibaba-cloud-file-storage-ten-opzichte-van-traditionele-file-storage)
    - [Welke best practices zijn er voor het gebruik van Alibaba Cloud File Storage in een microservices-architectuur?](#welke-best-practices-zijn-er-voor-het-gebruik-van-alibaba-cloud-file-storage-in-een-microservices-architectuur)
    - [Hoe kan Alibaba Cloud File Storage worden geïntegreerd in een al bestaande self-managed microservices-architectuur?](#hoe-kan-alibaba-cloud-file-storage-worden-geïntegreerd-in-een-al-bestaande-self-managed-microservices-architectuur)
      - [Stap 1: Maak een RAM-gebruiker aan](#stap-1-maak-een-ram-gebruiker-aan)
      - [Stap 2: Koppel de policy aan de RAM-gebruiker](#stap-2-koppel-de-policy-aan-de-ram-gebruiker)
      - [Stap 3: Maak een secret aan in Kubernetes](#stap-3-maak-een-secret-aan-in-kubernetes)
      - [Stap 4: Installeer de CSI-plug-in](#stap-4-installeer-de-csi-plug-in)
    - [Conclusie](#conclusie)
  - [Bronnen](#bronnen)

## Het toepassen van Alibaba Cloud File Storage in een self-managed microservices-architectuur

Voor dit onderzoek is gekeken naar hoe je Alibaba Cloud File Storage kunt toepassen in een self-managed microservices-architectuur. Hierbij hebben we gekeken naar de belangrijkste kenmerken en mogelijkheden van Alibaba Cloud File Storage, de voordelen ten opzichte van traditionele file storage, best practices voor het gebruik van Alibaba Cloud File Storage in een microservices-architectuur, en hoe je Alibaba Cloud File Storage kunt integreren in een al bestaande self-managed microservices-architectuur.

In de wereld van moderne softwareontwikkeling spelen cloud-native applicaties en microservices-architecturen een cruciale rol. Bedrijven verplaatsen hun infrastructuur steeds meer naar de cloud vanwege de flexibiliteit, schaalbaarheid en kostenefficiëntie. Een belangrijk aspect van deze transformatie is bestandsopslag: hoe beheer je grote hoeveelheden data die toegankelijk moeten zijn voor meerdere services, verspreid over verschillende omgevingen?

Hier komt Alibaba Cloud File Storage in beeld. Als een van de belangrijkste producten van Alibaba Cloud, biedt het een robuuste oplossing voor bedrijven die op zoek zijn naar schaalbare en betrouwbare opslag in hun microservices-architectuur. In deze blog verkennen we hoe je Alibaba Cloud File Storage kunt toepassen binnen een microservices-architectuur, en bekijken we de voordelen, best practices, en de integratiemogelijkheden.

### Wat zijn de belangrijkste kenmerken en mogelijkheden van Alibaba Cloud File Storage?

Alibaba Cloud File Storage, ook wel bekend als Alibaba Cloud NAS (Network Attached Storage), biedt gedeelde bestandsopslag die toegankelijk is vanuit verschillende compute-resources zoals Kubernetes-pods, ECI (Elastic Container Instances) en VM’s. Dit maakt het bij uitstek geschikt voor microservices-architecturen, waar verschillende services gelijktijdig toegang moeten hebben tot gedeelde gegevens.

De structuur in het voorbeeld illustreert hoe traditionele architecturen kunnen profiteren van een modernere benadering, waarbij bestanden worden ontsloten via een gedeelde opslagoplossing. Dit verbetert de veerkracht van systemen en ondersteunt een naadloze migratie naar schaalbare microservices.

<img src="plaatjes/opzet applicatie.webp" title="Opzet applicatie structuur">

Belangrijke kenmerken van Alibaba Cloud File Storage zijn:

- Schaalbaarheid: De opslag groeit automatisch mee met je behoeften. Dit betekent dat je je geen zorgen hoeft te maken over de capaciteit, zelfs niet bij snelle uitbreiding van je microservices.
- Flexibele toegang: Alibaba Cloud File Storage ondersteunt meerdere toegangspunten, zoals NFS (Network File System), wat het mogelijk maakt om eenvoudig gedeelde opslag in te zetten en de Container Storage Interface (CSI) plug-in voor Kubernetes.
- Hoge betrouwbaarheid: Met 99,9999999% (9-nines) databetrouwbaarheid, biedt het een hoge mate van zekerheid dat je data correct is.
- Hoge beschikbaarheid: Alibaba Cloud File Storage is ontworpen om hoge beschikbaarheid te bieden, met een SLA van 99,9% uptime.
- Beveiliging: Door functies zoals automatische versleuteling van gegevens tijdens transport en rust, voldoet Alibaba Cloud File Storage aan strikte beveiligingsnormen, wat belangrijk is voor microservices die gevoelige informatie verwerken.
- Lage kosten: Door het pay-as-you-go-model van Alibaba Cloud, betaal je alleen voor wat je gebruikt, waardoor je kosten laag blijven.

### Welke voordelen biedt Alibaba Cloud File Storage ten opzichte van traditionele file storage?

Traditionele opslagoplossingen, zoals fysieke NAS-systemen of on-premise storage, hebben verschillende beperkingen in een cloud- en microservices-gebaseerde architectuur. Deze traditionele oplossingen vereisen vaak veel onderhoud, handmatige schaling, en bieden beperkte flexibiliteit bij het delen van bestanden tussen verschillende services.

Alibaba Cloud File Storage biedt enkele duidelijke voordelen ten opzichte van traditionele file storage-oplossingen:

- Automatische schaalbaarheid: Terwijl traditionele opslag vaak op vaste capaciteit draait, kun je bij Alibaba Cloud File Storage vrijwel onbeperkt schalen zonder de noodzaak om hardware-upgrades uit te voeren.
- Eenvoudige integratie met cloud-native tools: Alibaba Cloud File Storage is volledig geïntegreerd met Alibaba's cloud ecosysteem. Dit maakt het gemakkelijk om opslag te beheren via geautomatiseerde workflows, zoals Kubernetes of DevOps CI/CD-pipelines.
- Lagere onderhoudskosten: Aangezien je geen fysieke infrastructuur hoeft te onderhouden, elimineert het gebruik van cloud-opslag veel van de overheadkosten en inspanningen die gepaard gaan met traditionele systemen.
- Betere toegankelijkheid en samenwerking: In een traditionele setup kunnen microservices die over verschillende geografische locaties draaien, beperkte toegang hebben tot on-premise storage. Met cloud-opslag, zoals Alibaba Cloud File Storage, kunnen services overal ter wereld veilig toegang krijgen tot dezelfde data.

### Welke best practices zijn er voor het gebruik van Alibaba Cloud File Storage in een microservices-architectuur?

Het correct toepassen van cloud-gebaseerde bestandsopslag in een microservices-architectuur vereist een zorgvuldige aanpak om prestatieproblemen en complexiteit te vermijden. Enkele best practices zijn:

- Data-isolatie per microservice: In een microservices-architectuur is het essentieel om de data van elke service te isoleren om onderlinge afhankelijkheden te vermijden. Alibaba Cloud File Storage kan worden gebruikt om opslagvolumes per microservice te creëren.
- Gebruik van Persistent Volumes (PVs) en Persistent Volume Claims (PVCs) in Kubernetes: In container-gebaseerde omgevingen, zoals Kubernetes, kun je Alibaba Cloud File Storage gebruiken via de Container Storage Interface (CSI). Door gebruik te maken van PV's en PVC's kun je eenvoudig opslag claimen voor elke microservice.
- Monitoring en optimalisatie: Zorg ervoor dat je de prestaties van je cloud-opslag monitort. Alibaba biedt tools zoals CloudMonitor waarmee je opslaggebruik, lees-/schrijfsnelheden, en fouten kunt bijhouden.
- Beveiliging van gevoelige data: Zorg ervoor dat je versleuteling inschakelt voor gevoelige gegevens, en beperk de toegang via role-based access control (RBAC) of IAM policies om ongeoorloofde toegang te voorkomen.

### Hoe kan Alibaba Cloud File Storage worden geïntegreerd in een al bestaande self-managed microservices-architectuur?

Als je al een microservices-architectuur hebt draaien binnen Alibaba Cloud, is het relatief eenvoudig om Alibaba Cloud File Storage te integreren. Met behulp van Kubernetes CSI-drivers kun je Alibaba Cloud File Storage eenvoudig als Persistent Volume (PV) mounten binnen je bestaande Kubernetes-cluster. Dit stelt je in staat om gedeelde opslag tussen verschillende microservices te configureren zonder downtime of grote veranderingen in je huidige infrastructuur.

Mocht je geen Kubernetes cluster in Alibaba Cloud hebben, dan kun je Alibaba Cloud File Storage ook integreren met een self-managed Kubernetes cluster. Het proces is vergelijkbaar, maar vereist enkele aanpassingen afhankelijk van de gebruikte tooling.

Een voorbeeld van hoe je Alibaba Cloud File Storage kunt integreren met een self-managed Kubernetes cluster is door middel van het mounten op een volume en het toewijzen van Persistent Volume Claims (PVCs) aan je services. Hiervoor moet je binnen Alibaba Cloud wel een gebruiker aanmaken en gebruikersrechten toewijzen zodat je verbinding kan maken met de managed cloud services van Alibaba Cloud. Hieronder volgen de stappen die je moet ondernemen om Alibaba Cloud File Storage te integreren in je bestaande self-managed microservices-architectuur:

#### Stap 1: Maak een RAM-gebruiker aan

Begin door een Resource Access Management (RAM)-gebruiker aan te maken in de Alibaba Cloud-console. Deze gebruiker heeft specifieke rechten nodig om toegang te krijgen tot de Alibaba Cloud File Storage-service.

Zodra de gebruiker is aangemaakt, moet je een custom policy definiëren die de juiste rechten toekent. Deze policy verleent toegang tot de NAS-service en stelt de gebruiker in staat acties uit te voeren zoals het maken van bestandssystemen en het mounten van volumes.

Een voorbeeld van een custom policy is hieronder weergegeven:

```json
{
  "Version": "1",
  "Statement": [
    {
      "Action": [
        "ecs:AttachDisk",
        "ecs:DetachDisk",
        "ecs:DescribeDisks",
        "ecs:CreateDisk",
        "ecs:ResizeDisk",
        "ecs:CreateSnapshot",
        "ecs:DeleteSnapshot",
        "ecs:CreateAutoSnapshotPolicy",
        "ecs:ApplyAutoSnapshotPolicy",
        "ecs:CancelAutoSnapshotPolicy",
        "ecs:DeleteAutoSnapshotPolicy",
        "ecs:DescribeAutoSnapshotPolicyEX",
        "ecs:ModifyAutoSnapshotPolicyEx",
        "ecs:AddTags",
        "ecs:DescribeTags",
        "ecs:DescribeSnapshots",
        "ecs:ListTagResources",
        "ecs:TagResources",
        "ecs:UntagResources",
        "ecs:ModifyDiskSpec",
        "ecs:CreateSnapshot",
        "ecs:DeleteDisk",
        "ecs:DescribeInstanceAttribute",
        "ecs:DescribeInstances"
      ],
      "Resource": ["*"],
      "Effect": "Allow"
    },
    {
      "Action": [
        "nas:DescribeFileSystems",
        "nas:DescribeMountTargets",
        "nas:AddTags",
        "nas:DescribeTags",
        "nas:RemoveTags",
        "nas:CreateFileSystem",
        "nas:DeleteFileSystem",
        "nas:ModifyFileSystem",
        "nas:CreateMountTarget",
        "nas:DeleteMountTarget",
        "nas:ModifyMountTarget",
        "nas:TagResources",
        "nas:SetDirQuota",
        "nas:EnableRecycleBin",
        "nas:GetRecycleBinAttribute"
      ],
      "Resource": ["*"],
      "Effect": "Allow"
    },
    {
      "Action": [
        "oss:PutBucket",
        "oss:GetObjectTagging",
        "oss:ListBuckets",
        "oss:PutBucketTags",
        "oss:GetBucketTags",
        "oss:PutBucketEncryption",
        "oss:GetBucketInfo"
      ],
      "Resource": ["*"],
      "Effect": "Allow"
    }
  ]
}
```

#### Stap 2: Koppel de policy aan de RAM-gebruiker

Nadat je de policy hebt aangemaakt, koppel je deze aan de RAM-gebruiker. Noteer de AccessKey en SecretKey van deze gebruiker, omdat je deze later nodig hebt voor authenticatie.

#### Stap 3: Maak een secret aan in Kubernetes

Gebruik de volgende opdracht om een secret aan te maken in je Kubernetes-cluster. Hiermee kun je de RAM-gebruiker authenticeren:

```bash
kubectl -n kube-system create secret generic alibaba-cloud-secret --from-literal='access-key-id=<your access key id>' --from-literal='access-key-secret=<your access key secret>'
```

#### Stap 4: Installeer de CSI-plug-in

Als laatste installeer je de Container Storage Interface (CSI)-plug-in. Gebruik hiervoor het onderstaande commando:

```bash
onectl addon install csi-plugin
```

Nadat de gebruiker is aangemaakt kun je bezig met een Alibaba Cloud File Storage-volume aanmaken. Dit kan het makkelijkst via de Alibaba Cloud-console. Maak een NAS-bestandssyteem aan in de gewenste regio en zorg dat je een VPC selecteert die wordt gebruikt door je Kubernetes-cluster. Dit volume kan vervolgens worden gemount op je Kubernetes-cluster. Zorg er wel voor dat je de NAS-bestandssysteem-ID en het NAS-mountpunt noteert. (Bijvoorbeeld: 0123456789 en 0123456789.ap-southeast-1.nas.aliyuncs.com)

Verbind via kubectl met je Kubernetes-cluster. Als je bent verbonden met je self-managed cluster kun je de Container Storage Interface (CSI) plug-in van Alibaba Cloud gebruiken. Daarna kun je een Persistent Volume (PV) definiëren dat verwijst naar je Alibaba Cloud File Storage-mount. In je eigen configuratie moet je nog het één en ander aanpassen om uiteindelijk te kunnen verbinden met je eigen NAS-bestandssysteem. Je moet in je Deployment-configuratie de omgevingsvariabelen ACCESS_KEY_ID en ACCESS_KEY_SECRET toevoegen die verwijzen naar de secret die je wilt toepassen op je mount. Omdat je gebruik maakt van de CSI plug-in hoef je verder geen authenticatie toe te passen in je PVC-configuratie. De RAM-user wordt namelijk via de Kubernetes Secret aan je CSI-driver gekoppeld. Wel moet je in je PV-configuratie het volumeHandle aanpassen naar de NAS-volume-handle die je hebt aangemaakt in je Alibaba Cloud-console en deze in je PVC en pod ook aanpassen.

Voorbeeld configuratie code kun je hieronder vinden:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: csi-alibaba-cloud
  namespace: kube-system
spec:
  containers:
    - name: nasplugin
      image: registry.cn-hangzhou.aliyuncs.com/acs/csi-plugin:<version>
      env:
        - name: ACCESS_KEY_ID
          valueFrom:
            secretKeyRef:
              name: alibaba-cloud-secret
              key: accessKeyId
        - name: ACCESS_KEY_SECRET
          valueFrom:
            secretKeyRef:
              name: alibaba-cloud-secret
              key: accessKeySecret
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: alibaba-nas-pv
spec:
  capacity:
    storage: 100Gi
  accessModes:
    - ReadWriteMany
  csi:
    driver: nasplugin.csi.alibabacloud.com
    volumeHandle: nas-volume-handle
    volumeAttributes:
      server: <nas-id>.cn-hangzhou.nas.aliyuncs.com # DNS-mountpoint
      path: <nas-file-system-path> # Pad in het NAS-bestandssysteem
  persistentVolumeReclaimPolicy: Retain
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: alibaba-nas-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 100Gi
  volumeName: alibaba-nas-pv
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-using-alibaba-nas
spec:
  containers:
    - name: app-container
      image: nginx
      volumeMounts:
        - name: nas-storage
          mountPath: "/mnt/nas"
  volumes:
    - name: nas-storage
      persistentVolumeClaim:
        claimName: alibaba-nas-pvc
```

Door deze eenvoudige stappen te volgen, kun je Alibaba Cloud File Storage snel en efficiënt integreren in je bestaande microservices-infrastructuur.

### Conclusie

Alibaba Cloud File Storage biedt een krachtige, schaalbare en veilige oplossing voor bedrijven die werken met een microservices-architectuur. Doordat je dit in combinatie kan gebruiken met zowel een self-managed kubernetes cluster als met een Alibaba ACK cluster kun je dit op verschillende manieren toepassen die bij je gewenste situatie passen. Door de flexibiliteit en integratiemogelijkheden van Alibaba Cloud File Storage kun je eenvoudig gedeelde bestandsopslag implementeren in je microservices-architectuur, zonder dat je je zorgen hoeft te maken over schaalbaarheid, betrouwbaarheid of beveiliging. Door de best practices te volgen en de integratiestappen te volgen, kun je snel aan de slag met het gebruik van Alibaba Cloud File Storage in je eigen microservices-architectuur. Doordat Alibaba Cloud File Storage gebruik maakt van RAM en Policy kun je de toegang makkelijk beheren en beveiligen. Tevens zorg je met de CSI plug-in voor naadloze integratie bij je al bestaande systeem.

## Bronnen

- ChatGPT - Onderzoek naar Alibaba Cloud. (10-10-2024). ChatGPT. [ChatGPT gesprek](https://chatgpt.com/share/67057fd3-82d8-8007-b8f8-f11df95f9414).
- Alibaba Cloud - Release notes for csi-plugin - Container Service for Kubernetes - Alibaba Cloud Documentation Center. (8-10-2024). [Alibaba csi-plugin](https://www.alibabacloud.com/help/en/ack/product-overview/csi-plugin)
- Cloud, A. Medium (2021, December 27). Alibaba Cloud File Storage NAS: Features, Benefits, Comparisons [Medium](https://alibaba-cloud.medium.com/alibaba-cloud-file-storage-nas-part-1-overview-and-explanation-3beb540125b4)
- Alibaba Cloud - Connect to an ACK cluster by using kubectl - Container Service for Kubernetes - Alibaba Cloud Documentation Center. (n.d.). [Alibaba ACK guide](https://www.alibabacloud.com/help/en/ack/serverless-kubernetes/user-guide/connect-to-an-ack-cluster-by-using-kubectl)
- Alibaba Cloud - Access a NAS file system from a data center by using a NAT gateway - Apsara File Storage NAS - Alibaba Cloud Documentation Center. (n.d.). [Alibaba NAS using NAT](https://www.alibabacloud.com/help/en/nas/user-guide/access-a-nas-file-system-from-a-data-center-through-a-nat-gateway)
- Alibaba Cloud - Mount a NAS file system by using the CSI plug-in provided by Alibaba Cloud - Apsara File Storage NAS - Alibaba Cloud Documentation Center. (n.d.). [Alibaba Cloud NAS CSI plug-in](https://www.alibabacloud.com/help/en/nas/user-guide/mount-nas-by-using-alibaba-cloud-csi-storage-components-recommend)
- Alibaba Cloud - What is a RAM user? - Resource Access Management - Alibaba Cloud Documentation Center. (n.d.). [Resource Access Manager](https://www.alibabacloud.com/help/en/ram/user-guide/overview-of-ram-users)
- Alibaba Cloud - Introduction to Apsara File Storage NAS - Alibaba Cloud Document Center. (n.d.).[Alibaba Learning Path](https://www.alibabacloud.com/help/en/nas/)
