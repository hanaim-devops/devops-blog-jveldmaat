# Alibaba Cloud File Storage in Microservices

<img src="plaatjes/alibaba_logo.png" width="250" align="right" alt="mdbook logo om weg te halen" title="maar vergeet de alt tekst niet">

*[Jesse Veldmaat, oktober 2024.](https://github.com/hanaim-devops/blog-student-naam)*
<hr/>

## Bronnen

- ChatGPT - Onderzoek naar Alibaba Cloud. (n.d.). ChatGPT. [ChatGPT gesprek](https://chatgpt.com/share/67057fd3-82d8-8007-b8f8-f11df95f9414).
- Release notes for csi-plugin - Container Service for Kubernetes - Alibaba Cloud Documentation Center. (n.d.). [Alibaba csi-plugin](https://www.alibabacloud.com/help/en/ack/product-overview/csi-plugin)
- Connect to an ACK cluster by using kubectl - Container Service for Kubernetes - Alibaba Cloud Documentation Center. (n.d.). [Alibaba ACK guide](https://www.alibabacloud.com/help/en/ack/serverless-kubernetes/user-guide/connect-to-an-ack-cluster-by-using-kubectl)
- Access a NAS file system from a data center by using a NAT gateway - Apsara File Storage NAS - Alibaba Cloud Documentation Center. (n.d.). [Alibaba NAS using NAT](https://www.alibabacloud.com/help/en/nas/user-guide/access-a-nas-file-system-from-a-data-center-through-a-nat-gateway)
- Mount a NAS file system by using the CSI plug-in provided by Alibaba Cloud - Apsara File Storage NAS - Alibaba Cloud Documentation Center. (n.d.). [Alibaba Cloud NAS CSI plug-in](https://www.alibabacloud.com/help/en/nas/user-guide/mount-nas-by-using-alibaba-cloud-csi-storage-components-recommend)
- What is a RAM user? - Resource Access Management - Alibaba Cloud Documentation Center. (n.d.). [Resource Access Manager](https://www.alibabacloud.com/help/en/ram/user-guide/overview-of-ram-users)

## Het toepassen van Alibaba Cloud File Storage in een self-managed microservices-architectuur

In de wereld van moderne softwareontwikkeling spelen cloud-native applicaties en microservices-architecturen een cruciale rol. Bedrijven verplaatsen hun infrastructuur steeds meer naar de cloud vanwege de flexibiliteit, schaalbaarheid en kostenefficiëntie. Een belangrijk aspect van deze transformatie is bestandsopslag: hoe beheer je grote hoeveelheden data die toegankelijk moeten zijn voor meerdere services, verspreid over verschillende omgevingen?

Hier komt Alibaba Cloud File Storage in beeld. Als een van de belangrijkste producten van Alibaba Cloud, biedt het een robuuste oplossing voor bedrijven die op zoek zijn naar schaalbare en betrouwbare opslag in hun microservices-architectuur. In deze blog verkennen we hoe je Alibaba Cloud File Storage kunt toepassen binnen een microservices-architectuur, en bekijken we de voordelen, best practices, en de integratiemogelijkheden.

### Wat zijn de belangrijkste kenmerken en mogelijkheden van Alibaba Cloud File Storage?

Alibaba Cloud File Storage, ook wel bekend als Alibaba Cloud NAS (Network Attached Storage), biedt gedeelde bestandsopslag die toegankelijk is vanuit verschillende compute-resources zoals Kubernetes-pods, ECI (Elastic Container Instances) en VM’s. Dit maakt het bij uitstek geschikt voor microservices-architecturen, waar verschillende services gelijktijdig toegang moeten hebben tot gedeelde gegevens.

Belangrijke kenmerken van Alibaba Cloud File Storage zijn:

- Schaalbaarheid: De opslag groeit automatisch mee met je behoeften. Dit betekent dat je je geen zorgen hoeft te maken over de capaciteit, zelfs niet bij snelle uitbreiding van je microservices.
- Flexibele toegang: Alibaba Cloud File Storage ondersteunt meerdere toegangspunten, zoals NFS (Network File System), wat het mogelijk maakt om eenvoudig gedeelde opslag in te zetten.
- Hoge beschikbaarheid en betrouwbaarheid: Met 99,9999999% (9-nines) gegevensduurzaamheid, biedt het een hoge mate van zekerheid dat je data altijd toegankelijk is, zelfs tijdens onderhoud of storingen.
- Beveiliging: Door functies zoals automatische versleuteling van gegevens tijdens transport en rust, voldoet Alibaba Cloud File Storage aan strikte beveiligingsnormen, wat belangrijk is voor microservices die gevoelige informatie verwerken.

### Welke voordelen biedt Alibaba Cloud File Storage ten opzichte van traditionele file storage?

Traditionele opslagoplossingen, zoals fysieke NAS-systemen of on-premise storage, hebben verschillende beperkingen in een cloud- en microservices-gebaseerde architectuur. Deze traditionele oplossingen vereisen vaak veel onderhoud, handmatige schaling, en bieden beperkte flexibiliteit bij het delen van bestanden tussen verschillende services.

Alibaba Cloud File Storage biedt enkele duidelijke voordelen ten opzichte van traditionele file storage-oplossingen:

- Automatische schaalbaarheid: Terwijl traditionele opslag vaak op vaste capaciteit draait, kun je bij Alibaba Cloud File Storage vrijwel onbeperkt schalen zonder de noodzaak om hardware-upgrades uit te voeren.
- Eenvoudige integratie met cloud-native tools: Alibaba Cloud File Storage is volledig geïntegreerd met Alibaba's cloud ecosysteem. Dit maakt het gemakkelijk om opslag te beheren via geautomatiseerde workflows, zoals Kubernetes of DevOps CI/CD-pipelines.
- Lagere onderhoudskosten: Aangezien je geen fysieke infrastructuur hoeft te onderhouden, elimineert het gebruik van cloud-opslag veel van de overheadkosten en inspanningen die gepaard gaan met traditionele systemen.
- Betere toegankelijkheid en samenwerking: In een traditionele setup kunnen microservices die over verschillende geografische locaties draaien, beperkte toegang hebben tot on-premise storage. Met cloud-opslag, zoals Alibaba Cloud File Storage, kunnen services overal ter wereld veilig toegang krijgen tot dezelfde data.

### Welke best practices zijn er voor het gebruik van Alibaba Cloud File Storage in een microservices-architectuur?

Het correct toepassen van cloud-gebaseerde bestandsopslag in een microservices-architectuur vereist een zorgvuldige aanpak om prestatieproblemen en complexiteit te vermijden. Enkele best practices zijn:

Data-isolatie per microservice: In een microservices-architectuur is het essentieel om de data van elke service te isoleren om onderlinge afhankelijkheden te vermijden. Alibaba Cloud File Storage kan worden gebruikt om opslagvolumes per microservice te creëren.
Gebruik van Persistent Volumes (PVs) en Persistent Volume Claims (PVCs) in Kubernetes: In container-gebaseerde omgevingen, zoals Kubernetes, kun je Alibaba Cloud File Storage gebruiken via de Container Storage Interface (CSI). Door gebruik te maken van PV's en PVC's kun je eenvoudig opslag claimen voor elke microservice.
Monitoring en optimalisatie: Zorg ervoor dat je de prestaties van je cloud-opslag monitort. Alibaba biedt tools zoals CloudMonitor waarmee je opslaggebruik, lees-/schrijfsnelheden, en fouten kunt bijhouden.
Beveiliging van gevoelige data: Zorg ervoor dat je versleuteling inschakelt voor gevoelige gegevens, en beperk de toegang via role-based access control (RBAC) of IAM policies om ongeoorloofde toegang te voorkomen.

### Hoe kan Alibaba Cloud File Storage worden geïntegreerd in een al bestaande self-managed microservices-architectuur?

Als je al een microservices-architectuur hebt draaien binnen Alibaba Cloud, is het relatief eenvoudig om Alibaba Cloud File Storage te integreren. Met behulp van Kubernetes CSI-drivers kun je Alibaba Cloud File Storage eenvoudig als Persistent Volume (PV) mounten binnen je bestaande Kubernetes-cluster. Dit stelt je in staat om gedeelde opslag tussen verschillende microservices te configureren zonder downtime of grote veranderingen in je huidige infrastructuur.

Mocht je geen Kubernetes cluster in Alibaba Cloud hebben, dan kun je Alibaba Cloud File Storage ook integreren met een self-managed Kubernetes cluster. Het proces is vergelijkbaar, maar vereist enkele aanpassingen afhankelijk van de gebruikte tooling.

Een voorbeeld van hoe je Alibaba Cloud File Storage kunt integreren met een self-managed Kubernetes cluster is door middel van het mounten op een volume en het toewijzen van Persistent Volume Claims (PVCs) aan je services. Hiervoor moet je binnen Alibaba Cloud wel een gebruiker aanmaken en gebruikersrechten toewijzen zodat je verbinding kan maken met de managed cloud services van Alibaba Cloud. Hieronder volgen de stappen die je moet ondernemen om Alibaba Cloud File Storage te integreren in je bestaande self-managed microservices-architectuur:

Je begint door een Resource Access Management (RAM) gebruiker aan te maken in de Alibaba Cloud-console. Deze gebruiker heeft de juiste rechten nodig om toegang te krijgen tot de Alibaba Cloud File Storage-service. Nadat de gebruiker is aangemaakt moet je een custom policy aanmaken die de nodige rechten toekent aan de gebruiker. Deze policy kan bijvoorbeeld toegang verlenen tot de NAS-service en de nodige acties toestaan, zoals het maken van bestandssystemen en het mounten van volumes (een voorbeeld van de policy staat hieronder aangegeven). Nadat de policy is aangemaakt, koppel je deze aan de RAM-gebruiker en noteer je de AccessKey en SecretKey van de gebruiker. Op basis hiervan kun je een secret aanmaken in je eigen Kubernetes cluster om de gebruiker te authenticeren. Met de volgende commando's kun je een secret aanmaken in Kubernetes:

```bash
kubectl -n kube-system create secret generic alibaba-cloud-secret --from-literal='access-key-id=<your access key id>' --from-literal='access-key-secret=<your access key secret>'
```

Als laatste moet je de CSI plug-in installeren. Dit kan met behulp van de volgende commando:

```bash
onectl addon install csi-plugin
```

Een voorbeeld code van de policy kan als volgt zijn:

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
            "Resource": [
                "*"
            ],
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
            "Resource": [
                "*"
            ],
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
            "Resource": [
                "*"
            ],
            "Effect": "Allow"
        }
    ]
}
```

Nadat de gebruiker is aangemaakt kun je bezig met een Alibaba Cloud File Storage-volume aanmaken. Dit kan het makkelijkst via de Alibaba Cloud-console. Maak een NAS-bestandssyteem aan in de gewenste regio en zorg dat je een VPC selecteert die wordt gebruikt door je Kubernetes-cluster. Dit volume kan vervolgens worden gemount op je Kubernetes-cluster. Zorg er wel voor dat je de NAS-bestandssysteem-ID en het NAS-mountpunt noteert. (Bijvoorbeeld: 0123456789 en 0123456789.ap-southeast-1.nas.aliyuncs.com)

Verbind via kubectl met je Kubernetes-cluster. Als je bent verbonden met je self-managed cluster kun je de Container Storage Interface (CSI) plug-in van Alibaba Cloud gebruiken. Daarna kun je een Persistent Volume (PV) definiëren dat verwijst naar je Alibaba Cloud File Storage-mount. In je eigen configuratie moet je nog het één en ander aanpassen om uiteindelijk te kunnen verbinden met je eigen NAS-bestandssysteem. Je moet in je Deployment-configuratie de omgevingsvariabelen ACCESS_KEY_ID en ACCESS_KEY_SECRET toevoegen die verwijzen naar de secret die je wilt toepassen op je mount. Omdat je gebruik maakt van de CSI plug-in hoef je verder geen authenticatie toe te passen in je PVC-configuratie. De RAM-user wordt namelijk via de Kubernetes Secret aan je CSI-driver gekoppeld.

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
      server: <nas-id>.cn-hangzhou.nas.aliyuncs.com  # DNS-mountpoint
      path: <nas-file-system-path>    # Pad in het NAS-bestandssysteem
  persistentVolumeReclaimPolicy: Retain
```

Stap 3: Maak Persistent Volume Claims (PVCs) aan voor je individuele microservices. Een voorbeeld van een PVC-configuratie kan zijn:

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

Nadat je de PVCs hebt aangemaakt pas je de Kubernetes deployment-configuraties aan om de PVC’s te gebruiken als mount points voor de services die toegang nodig hebben tot de opslag. Een voorbeeld van een pod-configuratie die gebruik maakt van de PVC kan zijn:

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

Alibaba Cloud File Storage biedt een krachtige, schaalbare en veilige oplossing voor bedrijven die werken met een microservices-architectuur. Door de naadloze integratie met cloud-native tools zoals Kubernetes en de vele voordelen ten opzichte van traditionele opslagoplossingen, is het een goede keuze om te overwegen. Hoewel het in een microservices-architectuur enige planning en configuratie vereist, biedt Alibaba Cloud File Storage de flexibiliteit en betrouwbaarheid die nodig zijn om succesvol te schalen in de cloud. Of je nu net begint met microservices of je huidige architectuur naar de cloud wilt verplaatsen, Alibaba Cloud File Storage biedt de flexibiliteit en betrouwbaarheid die je nodig hebt om succesvol te schalen.
