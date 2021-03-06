# Szyfrowanie

Kubernetes przechowuje różne dane - stan klastra, konfigurację aplikacji i sekrety. Zaszyfrujmy to!

## Encryption Key
Tworzymy klucz szyfrowania dla secretów:
```
ENCRYPTION_KEY=$(head -c 32 /dev/urandom | base64)
```
## Encryption Config File

Manifest dla konfiguracji szyfrowania K8S:
```
cat > encryption-config.yaml <<EOF
kind: EncryptionConfig
apiVersion: v1
resources:
  - resources:
      - secrets
    providers:
      - aescbc:
          keys:
            - name: key1
              secret: ${ENCRYPTION_KEY}
      - identity: {}
EOF
```
Kopjujemy manifest do serwera master01:
```
scp -i ../Kubernetes_Fundamentals.pem encryption-config.yaml ubuntu@${MASTER01_IP}:~
```
## Podsumowanie
Zasady szyfrowania i klucz ustawionym czas na uruchomienie bazy danych, czyli [etcd](https://github.com/inleo-pl/Warsztat-Kubernetes-Fundamentals/blob/master/06-Uruchomienie-etcd.md).
