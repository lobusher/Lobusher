import { useState } from "react"; import { Button } from "@/components/ui/button"; import { Card, CardContent } from "@/components/ui/card"; import { motion } from "framer-motion"; import { FaWallet } from "react-icons/fa"; import Image from "next/image";

export default function LobusherLanding() { const [walletConnected, setWalletConnected] = useState(false);

const connectWallet = async () => { if (typeof window.ethereum !== "undefined") { try { await window.ethereum.request({ method: "eth_requestAccounts" }); setWalletConnected(true); } catch (error) { console.error("Connection error:", error); } } else { alert("MetaMask не установлен"); } };

return ( <div className="min-h-screen bg-gradient-to-br from-[#1e1e2f] to-[#0c0c15] text-white p-6 flex flex-col items-center justify-center"> <motion.h1 initial={{ opacity: 0, y: -40 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.8 }} className="text-5xl font-bold mb-4 text-orange-400" > LOBUSHER </motion.h1>

<Image
    src="/lobusher.png"
    alt="Lobusher"
    width={300}
    height={300}
    className="rounded-2xl shadow-lg mb-6"
  />

  <p className="text-xl mb-4 max-w-xl text-center">
    Добро пожаловать в мир Lobusher. Мистический токен $LOBU с философией магии и хаоса. Покупай, храни, исследуй.
  </p>

  <div className="flex gap-4 mb-6">
    <Button onClick={connectWallet} className="bg-orange-500 hover:bg-orange-600 text-lg">
      <FaWallet className="mr-2" />
      {walletConnected ? "Кошелёк подключён" : "Подключить MetaMask"}
    </Button>

    <a
      href="https://pancakeswap.finance/swap?outputCurrency=0xYourTokenAddress"
      target="_blank"
      rel="noopener noreferrer"
    >
      <Button className="bg-green-500 hover:bg-green-600 text-lg">
        Купить $LOBU
      </Button>
    </a>
  </div>

  <Card className="bg-[#2e2e3d] text-white max-w-xl">
    <CardContent className="p-6">
      <h2 className="text-2xl font-bold mb-2">📜 Whitepaper</h2>
      <p className="mb-4">
        Ознакомься с полной философией и токеномикой Lobusher. Узнай, как он свяжет мир NFT, Web3 и магии.
      </p>
      <a
        href="/whitepaper.pdf"
        download
        className="underline text-orange-400 hover:text-orange-300"
      >
        Скачать Whitepaper
      </a>
    </CardContent>
  </Card>
</div>

); }

