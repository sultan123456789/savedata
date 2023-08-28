## Pastikan Anda nambahkan file javascript pada `README.md` master agar bekerja pada index.html lalu tambahkan pada bagian body index.html :

## Pastikan sudah memiliki akun sepolia testnet ethereum pada metamask/daftar disini : https://www.alchemy.com/overviews/how-to-add-sepolia-to-metamask

## Mengatur Kontrak Pintar dan Provider

Pada bagian `<script>` di bawah impor pustaka ethers.js, Anda akan melihat kode yang mengatur kontrak pintar dan provider Ethereum. Pastikan Anda telah memasukkan alamat kontrak (`MoodContractAddress`) dan ABI kontrak (`MoodContractABI`) sesuai dengan kontrak pintar Anda.

## Interaksi dengan Kontrak

Anda memiliki dua fungsi utama yang dapat digunakan:

1. **getMood():** Fungsi ini akan mengambil data mood, nama, dan alamat yang tersimpan di kontrak dan menampilkannya di konsol browser Anda.

```
 async function getMood() {
          const moodPromise = MoodContract.getMood();
          const namePromise = MoodContract.name();
          const alamatPromise = MoodContract.alamat();
          const [mood, name, alamat] = await Promise.all([moodPromise, namePromise, alamatPromise]);
          console.log(`Mood: ${mood}, Name: ${name}, Alamat: ${alamat}`);
         // const tx = await provider.getTransactionReceipt(txHash);
          //console.log(`Transaction hash: ${tx.hash}`);
        }
```


3. **setData():** Fungsi ini memungkinkan Anda untuk mengatur data mood, nama, dan alamat dengan memanggil fungsi `setMood()` pada kontrak. Isikan nilai mood, nama, dan alamat di bidang input pada halaman HTML Anda, kemudian klik tombol "Set Data" untuk mengirim data baru ke kontrak.

```
 async function setData() {
          const mood = document.getElementById("mood").value;
          const name = document.getElementById("name").value;
          const alamat = document.getElementById("alamat").value;
          const tx = await MoodContract.setMood(mood, name, alamat);
          const setMoodPromise = MoodContract.setMood(mood, name, alamat);
          await setMoodPromise;
          console.log(`Transaction hash: ${tx.hash}`);
        }
```

## Menjalankan Aplikasi

Buka file `index.html` di browser Anda. Anda akan melihat tampilan antarmuka sederhana dengan bidang input untuk mood, nama, dan alamat, serta tombol untuk mengirim data. Pastikan Anda juga membuka konsol pengembang pada browser Anda untuk melihat hasil dari interaksi dengan kontrak.

## Kontribusi

Jika Anda ingin berkontribusi pada pengembangan aplikasi ini, jangan ragu untuk melakukan _pull request_ dengan perubahan atau peningkatan yang Anda usulkan. Kami menyambut kontribusi dari semua tingkat keahlian!

## Lisensi

Aplikasi ini dilisensikan di bawah Lisensi MIT - lihat berkas [LICENSE](LICENSE) untuk detail lebih lanjut.

## Full Script

```
<script src="https://cdn.ethers.io/lib/ethers-5.2.umd.min.js" type="application/javascript"></script>
      <script>
        const provider = new ethers.providers.Web3Provider(
          window.ethereum,
          "any"
        );
    
       // const MoodContractAddress = "0x4A2f7fc4aCb5c2cf4C2a9af0341b2B2F7E8E5Dd1";
       const MoodContractAddress = "0x42d2031EBf78C5Cc9C015305840667B722ad140c";
        const MoodContractABI = [
        {
          "inputs": [
            {
              "internalType": "string",
              "name": "_mood",
              "type": "string"
            },
            {
              "internalType": "string",
              "name": "_name",
              "type": "string"
            },
            {
              "internalType": "string",
              "name": "_alamat",
              "type": "string"
            }
          ],
          "name": "setMood",
          "outputs": [],
          "stateMutability": "nonpayable",
          "type": "function"
        },
        {
          "inputs": [],
          "name": "alamat",
          "outputs": [
            {
              "internalType": "string",
              "name": "",
              "type": "string"
            }
          ],
          "stateMutability": "view",
          "type": "function"
        },
        {
          "inputs": [],
          "name": "getMood",
          "outputs": [
            {
              "internalType": "string",
              "name": "",
              "type": "string"
            }
          ],
          "stateMutability": "view",
          "type": "function"
        },
        {
          "inputs": [],
          "name": "mood",
          "outputs": [
            {
              "internalType": "string",
              "name": "",
              "type": "string"
            }
          ],
          "stateMutability": "view",
          "type": "function"
        },
        {
          "inputs": [],
          "name": "name",
          "outputs": [
            {
              "internalType": "string",
              "name": "",
              "type": "string"
            }
          ],
          "stateMutability": "view",
          "type": "function"
        }
      ];
    
        let MoodContract;
        let signer;
          provider.send("eth_requestAccounts", []).then(() => {
          provider.listAccounts().then(function (accounts) {
            signer = provider.getSigner(accounts[0]);
            MoodContract = new ethers.Contract(
              MoodContractAddress,
              MoodContractABI,
              signer
            );
          });
        });
    
        async function getMood() {
          const moodPromise = MoodContract.getMood();
          const namePromise = MoodContract.name();
          const alamatPromise = MoodContract.alamat();
          const [mood, name, alamat] = await Promise.all([moodPromise, namePromise, alamatPromise]);
          console.log(`Mood: ${mood}, Name: ${name}, Alamat: ${alamat}`);
         // const tx = await provider.getTransactionReceipt(txHash);
          //console.log(`Transaction hash: ${tx.hash}`);
        }
          async function setData() {
          const mood = document.getElementById("mood").value;
          const name = document.getElementById("name").value;
          const alamat = document.getElementById("alamat").value;
          const tx = await MoodContract.setMood(mood, name, alamat);
          const setMoodPromise = MoodContract.setMood(mood, name, alamat);
          await setMoodPromise;
          console.log(`Transaction hash: ${tx.hash}`);
        }
        </script>
      <script src="app.js"></script>
```
