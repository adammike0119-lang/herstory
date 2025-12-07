# herstoryimport React, { useState, useEffect, useRef } from 'react';
import { 
  Heart, 
  ShoppingBag, 
  Menu, 
  Search, 
  User, 
  Play, 
  Pause, 
  Mic, 
  Camera, 
  Sparkles, 
  CheckCircle, 
  ArrowRight,
  Briefcase,
  Globe,
  DollarSign,
  Edit3,
  Image as ImageIcon,
  ChevronLeft,
  Settings,
  MessageSquare,
  LogOut,
  X,
  Send,
  Loader,
  Filter,
  Trash2,
  CreditCard,
  MapPin,
  Gift,
  FileText,
  Smile
} from 'lucide-react';

// --- 模擬資料庫 (Mock Data) ---
const CREATORS = [
  {
    id: 1,
    name: "林秀琴",
    title: "再生布藝師",
    avatar: "https://cms-artifacts.artlist.io/content/generated-image-v1/image__7/generated-image-bf1332d7-d66d-4d7d-9727-73cc113640ad.png?Expires=2080483061&Key-Pair-Id=K2ZDLYDZI2R1DF&Signature=Gn0Vsr9huNzrmnEX68W4FhMsPVqjL53bTOleEbawvX2UDwavn1T8y1MHgLIcdcvy5WeNOozfLuZRr5Yvw7qpZNu5rY0yD~BPENciHgn3SeLwNKWm8sPjvYAPWf04xD~6nyr6DDQ~d6ABTFSLjTudrXkmBt~47fao1OTIY8ATaIRU0KwYPG1iOEAeJNFuLNG4Cwx0QlfesJhhIipexIEaCpUgDiR1Y6hiAzHnR7l-M6x2wYmzeAI-zGeqBwAb9V-KMs7a17DsyHFHhn4VTsCuvCPmADrOIjBgumOLY0V-8seRJCmBDz5WzYBobMWaBz9eXRw1XYT5-bmxW0hQAZ8adQ__",
    heroImage: "https://cms-artifacts.artlist.io/content/generated-image-v1/image__7/generated-image-bf1332d7-d66d-4d7d-9727-73cc113640ad.png?Expires=2080483061&Key-Pair-Id=K2ZDLYDZI2R1DF&Signature=Gn0Vsr9huNzrmnEX68W4FhMsPVqjL53bTOleEbawvX2UDwavn1T8y1MHgLIcdcvy5WeNOozfLuZRr5Yvw7qpZNu5rY0yD~BPENciHgn3SeLwNKWm8sPjvYAPWf04xD~6nyr6DDQ~d6ABTFSLjTudrXkmBt~47fao1OTIY8ATaIRU0KwYPG1iOEAeJNFuLNG4Cwx0QlfesJhhIipexIEaCpUgDiR1Y6hiAzHnR7l-M6x2wYmzeAI-zGeqBwAb9V-KMs7a17DsyHFHhn4VTsCuvCPmADrOIjBgumOLY0V-8seRJCmBDz5WzYBobMWaBz9eXRw1XYT5-bmxW0hQAZ8adQ__",
    story: "我的一生都在與布料對話。年輕時在成衣廠車縫，現在我收集舊和服與廢棄布料，將它們拆解、清洗，重新拼貼成有溫度的生活小物。每一個拼布包，都藏著一段被遺忘的時光，我希望能透過雙手，讓這些布料重獲新生。",
    tags: ["環保再生", "傳統拼布", "客製化"],
    audioTitle: "EP.1 布料的記憶與新生命",
    audioDuration: "03:45",
    products: [
      { id: 101, title: "昭和風再生拼布包", price: 1280, image: "https://images.unsplash.com/photo-1590874103328-eac38a683ce7?auto=format&fit=crop&q=80&w=400&h=400" }, 
      { id: 102, title: "手作藍染杯墊組", price: 450, image: "https://cms-artifacts.artlist.io/content/generated-image-v1/image__5/generated-image-02895c87-b4b5-4ef5-8714-9c1eca59e81b.png?Expires=2080480487&Key-Pair-Id=K2ZDLYDZI2R1DF&Signature=UqhH4Ab0dCk-Il94nAXMZq3VX-Z3RgeBI~dWqwDsuW81TQw3UcLd-GaD-iwOx3QQBewfML585Onu2oMbCWd-6mpO2NjFzp8xWs9GGNHb3KYtlYiCwuSj7RYZvCxkTcKdI38n3vTMiTKA2sO441-jT-k9BGgj~0LiNzP9jEM~bhUuym-gSijT8WBFG8iFuajlyAelvx3dk734gBtnUXzkF~9gTk45NncK01ocm1Qqf5Cj3IW4O9Y0fcII99pVnsRM91TRfrolhMbq4n8RrmNG01AcyWn4uuPk6kGoOH01gksuD9Rd~AbxzIUhZqXvC-rTRlPVkIdKuJLdzWQLudnrXw__" }, 
      { id: 103, title: "復古花布口金包", price: 880, image: "https://cms-artifacts.artlist.io/content/generated-image-v1/image__7/generated-image-7999d082-a4ed-46c2-900b-c546d061f5ae.png?Expires=2080480749&Key-Pair-Id=K2ZDLYDZI2R1DF&Signature=W7YIRzOKrYKHSnpW5kzX9M60VpW-C6-ZO7CrhYcwZkC46S5bxOC6Xf2jmWhLagCdKVTRdNGcGCEgL0PAKTPIu6kvIZOT9d6lWCCQVQl0wracGDJZK3DQqWYY3NodnBe6Hed3PgMk4h~YxgNvca7i9dnVo0hB6D4Qbe~UAnBkdjHafzU-SjOGETDyXe4QPB8mJHx5ZiEueqk2c4KhrPvRSPnrg~uMdu7dadTw78Yvt3XfkcLrboPMlf8hbvcAtKQLQ6rrkrgBTU2Xs3sXNZRc5WNIzWEqk0KZiEQGdzwfLpF~Lc2zGcrJ~k5yCuZNgRiNx0M4VZ5E8BErBICTCOSg0A__" } 
    ]
  },
  {
    id: 2,
    name: "張美蘭",
    title: "部落編織傳承者",
    avatar: "https://cms-artifacts.artlist.io/content/generated-image-v1/image__1/generated-image-95b7cc5d-d6ab-4548-8016-136d440ae05e.png?Expires=2080483240&Key-Pair-Id=K2ZDLYDZI2R1DF&Signature=gaQn0HQNMREFwCVynNtI5DIVkKxkS6hPzYzCTb2ptHfhkJGxGaUrIXS-AV8E5t7pJTFPA6tUH1nEKz6wf5TEUl6xF0DuXlVDhV76NLuKVLyEyPMP62vund3wSNbl0Z2l7Zb1XWgTb3WK9ujVSe3iur4ufWM6mCcZH7F4qwTqMmlLbzVLrWqf7ZmwWWqnjZKIx79cTEKOAxnex2LvVElSSfmMIeWFs6kzH1lez0pYy5lreEmH0sS2sWVvnYcg7cUeJumiRxaWFYEUYxNNOQTatVkdZYDlv3heg59SQLsy5Hmpq9sft~H7OxNZ~j7VUbMac44XejtfDsUE6cbx1piing__",
    heroImage: "https://cms-artifacts.artlist.io/content/generated-image-v1/image__1/generated-image-95b7cc5d-d6ab-4548-8016-136d440ae05e.png?Expires=2080483240&Key-Pair-Id=K2ZDLYDZI2R1DF&Signature=gaQn0HQNMREFwCVynNtI5DIVkKxkS6hPzYzCTb2ptHfhkJGxGaUrIXS-AV8E5t7pJTFPA6tUH1nEKz6wf5TEUl6xF0DuXlVDhV76NLuKVLyEyPMP62vund3wSNbl0Z2l7Zb1XWgTb3WK9ujVSe3iur4ufWM6mCcZH7F4qwTqMmlLbzVLrWqf7ZmwWWqnjZKIx79cTEKOAxnex2LvVElSSfmMIeWFs6kzH1lez0pYy5lreEmH0sS2sWVvnYcg7cUeJumiRxaWFYEUYxNNOQTatVkdZYDlv3heg59SQLsy5Hmpq9sft~H7OxNZ~j7VUbMac44XejtfDsUE6cbx1piing__",
    story: "從阿嬤那裡學來的編織技法，不能在我這代斷掉。我嘗試結合現代強韌的傘繩與傳統圖騰，做成適合都會人使用的飲料提袋與背帶。這不僅是商品，更是部落的祝福與山林的禮物。",
    tags: ["原民工藝", "戶外實用", "文化傳承"],
    audioTitle: "EP.5 山林裡的編織歌",
    audioDuration: "05:20",
    products: [
      { id: 201, title: "圖騰編織水壺袋", price: 680, image: "https://cms-artifacts.artlist.io/content/generated-image-v1/image__5/generated-image-ba5ffd74-a41a-4a94-9161-e60b0fcbd489.png?Expires=2080482891&Key-Pair-Id=K2ZDLYDZI2R1DF&Signature=xagHg5b4fCQiOhp4O7ekMFLOphJP4LAFPPVba6~E5Jyy3hbgQTm95X-8O6pLJpZowMxPJH3rMaLbs9ZNvIXOcfJS7UOyLeI-~c7wamvCQKdCHxdy7OruUb2LBpB-O94ptNcOmur3ahwscCkbiny03CfJ97myklntmuFajJ-O28unTTcjSc6OGFH93buhR92LNW-hckG9cSY7d5oJEdG4LmB71LLsb6zv2Js0imxallxbge5K-1Q32j~iMxU7u2OSMfriaiaQUptlTA4dYbnaWnVFZBtcgKWQ1-hVHsR9Sv2GrPHzfczIPObIvodxdgAeYHsjey6FlJ5qA4oS6lmuYA__" },
      { id: 202, title: "強韌登山背帶", price: 950, image: "https://images.unsplash.com/photo-1551232864-3f0890e580d9?auto=format&fit=crop&q=80&w=400&h=400" } 
    ]
  }
];

const THEMES = [
  { id: 'heritage', title: '傳承', desc: '延續百年的技藝與溫度', img: 'https://images.unsplash.com/photo-1544365558-35aa4afcf11f?auto=format&fit=crop&q=80&w=600' },
  { id: 'newlife', title: '新生', desc: '賦予舊物第二次的生命', img: 'https://images.unsplash.com/photo-1516975080664-ed2fc6a32937?auto=format&fit=crop&q=80&w=600' },
  { id: 'power', title: '女力', desc: '溫柔而堅韌的女性力量', img: 'https://images.unsplash.com/photo-1573164713714-d95e436ab8d6?auto=format&fit=crop&q=80&w=600' }
];

const MOCK_ORDERS = [
  { id: 'ORD-001', item: '客製化拼布包 (藍色系)', status: '待確認', date: '2023-10-24', buyer: '陳小姐', details: '希望能放下 A4 文件夾，背帶加寬。', price: 1580 },
  { id: 'ORD-002', item: '手作藍染杯墊組 x 2', status: '已出貨', date: '2023-10-23', buyer: '王先生', details: '一般標準款，無特殊需求。', price: 900 }
];

const MOCK_USER_ORDERS = [
  { id: 'MY-001', date: '2023-10-15', total: 1280, status: '已送達', items: ['昭和風再生拼布包'] },
  { id: 'MY-002', date: '2023-09-20', total: 450, status: '已完成', items: ['手作藍染杯墊組'] }
];

// --- 共用元件：通知訊息 (Toast) ---
const Toast = ({ message, type = 'success', onClose }) => {
  useEffect(() => {
    const timer = setTimeout(onClose, 3000);
    return () => clearTimeout(timer);
  }, [onClose]);

  return (
    <div className={`fixed top-20 right-4 z-[70] px-6 py-3 rounded-lg shadow-xl flex items-center gap-3 animate-in slide-in-from-right duration-300 ${type === 'success' ? 'bg-stone-800 text-white' : 'bg-red-500 text-white'}`}>
      {type === 'success' ? <CheckCircle size={20} /> : <X size={20} />}
      <span className="font-medium">{message}</span>
    </div>
  );
};

// --- 共用元件：彈窗 (Modal) ---
const Modal = ({ isOpen, onClose, title, children }) => {
  if (!isOpen) return null;
  return (
    <div className="fixed inset-0 z-[60] flex items-center justify-center bg-black/50 backdrop-blur-sm p-4 animate-in fade-in duration-200">
      <div className="bg-white rounded-xl shadow-2xl w-full max-w-md overflow-hidden animate-in zoom-in-95 duration-200 max-h-[90vh] overflow-y-auto">
        <div className="flex justify-between items-center p-4 border-b sticky top-0 bg-white z-10">
          <h3 className="font-bold text-lg">{title}</h3>
          <button onClick={onClose} className="p-1 hover:bg-stone-100 rounded-full"><X size={20}/></button>
        </div>
        <div className="p-4">{children}</div>
      </div>
    </div>
  );
};

// --- 元件：AI 客服機器人 (浮動式) ---
const AiChatBot = ({ type = 'customer', onNotify }) => {
  const [isOpen, setIsOpen] = useState(false);
  const [messages, setMessages] = useState([
    { role: 'ai', text: type === 'customer' 
      ? '您好！我是 HerStory 客服機器人。想找什麼樣的故事或作品嗎？我可以幫您推薦喔！' 
      : '秀琴姐您好！我是您的創作小幫手。今天想寫什麼故事，或是需要計算成本嗎？' 
    }
  ]);
  const [input, setInput] = useState('');
  const messagesEndRef = useRef(null);

  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
  };

  useEffect(scrollToBottom, [messages, isOpen]);

  const handleSend = () => {
    if (!input.trim()) return;
    const newMsgs = [...messages, { role: 'user', text: input }];
    setMessages(newMsgs);
    setInput('');

    // 模擬 AI 回覆
    setTimeout(() => {
      let reply = '';
      if (type === 'customer') {
        if (input.includes('客製化')) reply = '您可以直接在創作者頁面點擊「我想客製化」按鈕，填寫您的需求，創作者會親自回覆您！';
        else if (input.includes('運費')) reply = '全站目前免運費活動進行中喔！';
        else if (input.includes('推薦') || input.includes('禮物')) reply = '如果是送禮，我非常推薦「手作藍染杯墊組」，實用又有溫度。或者您可以看看「主題展間」找靈感！';
        else reply = '這是個好問題！我已經幫您記錄下來，轉交給創作者或平台管理員處理。';
      } else {
        if (input.includes('文案')) reply = '沒問題，您可以試著描述一下作品的材質和製作心情，我來幫您潤飾！';
        else if (input.includes('價格')) reply = '建議您使用「上傳新作品」功能的 AI 定價師，我會幫您精算工時與材料喔！';
        else reply = '收到！這聽起來很棒，加油！';
      }
      setMessages([...newMsgs, { role: 'ai', text: reply }]);
    }, 1000);
  };

  return (
    <>
      <button 
        onClick={() => setIsOpen(!isOpen)}
        className={`fixed bottom-6 right-6 z-50 p-4 rounded-full shadow-xl transition-all hover:scale-110 flex items-center justify-center ${type === 'customer' ? 'bg-rose-600 text-white' : 'bg-indigo-600 text-white'}`}
      >
        {isOpen ? <X size={24} /> : <MessageSquare size={24} />}
        {!isOpen && <span className="absolute -top-1 -right-1 flex h-3 w-3"><span className="animate-ping absolute inline-flex h-full w-full rounded-full bg-white opacity-75"></span><span className="relative inline-flex rounded-full h-3 w-3 bg-red-400"></span></span>}
      </button>

      {isOpen && (
        <div className="fixed bottom-24 right-6 z-50 w-80 md:w-96 bg-white rounded-2xl shadow-2xl border border-stone-200 overflow-hidden flex flex-col h-[400px] animate-in slide-in-from-bottom-5 duration-200">
          <div className={`p-4 ${type === 'customer' ? 'bg-rose-600' : 'bg-indigo-600'} text-white flex items-center gap-2`}>
            <Sparkles size={18} />
            <span className="font-bold">{type === 'customer' ? 'AI 客服小幫手' : '創作靈感夥伴'}</span>
            <button onClick={() => setIsOpen(false)} className="ml-auto hover:bg-white/20 rounded-full p-1"><X size={16}/></button>
          </div>
          <div className="flex-1 overflow-y-auto p-4 space-y-4 bg-stone-50">
            {messages.map((msg, idx) => (
              <div key={idx} className={`flex ${msg.role === 'user' ? 'justify-end' : 'justify-start'}`}>
                <div className={`max-w-[80%] p-3 rounded-xl text-sm ${msg.role === 'user' ? 'bg-stone-800 text-white' : 'bg-white text-stone-800 shadow-sm border border-stone-100'}`}>
                  {msg.text}
                </div>
              </div>
            ))}
            <div ref={messagesEndRef} />
          </div>
          <div className="p-3 bg-white border-t flex gap-2">
            <input 
              type="text" 
              value={input}
              onChange={e => setInput(e.target.value)}
              onKeyPress={e => e.key === 'Enter' && handleSend()}
              placeholder="輸入訊息..."
              className="flex-1 bg-stone-100 rounded-full px-4 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-rose-500"
            />
            <button onClick={handleSend} className={`p-2 rounded-full ${type === 'customer' ? 'text-rose-600 hover:bg-rose-50' : 'text-indigo-600 hover:bg-indigo-50'}`}>
              <Send size={20} />
            </button>
          </div>
        </div>
      )}
    </>
  );
};

// --- 元件：創作者登入介面 ---
const CreatorLogin = ({ onLogin, onSwitchMode, onNotify }) => {
  const [account, setAccount] = useState('creator');
  const [password, setPassword] = useState('');
  const [isLoading, setIsLoading] = useState(false);

  const handleSubmit = (e) => {
    e.preventDefault();
    setIsLoading(true);
    setTimeout(() => {
      if (account && password) {
        onLogin();
        onNotify("登入成功！歡迎回到創作者工坊");
      } else {
        onNotify("請輸入帳號與密碼", "error");
        setIsLoading(false);
      }
    }, 1000);
  };

  return (
    <div className="min-h-screen flex items-center justify-center bg-stone-100 p-4">
      <div className="bg-white p-8 rounded-2xl shadow-xl w-full max-w-sm animate-in zoom-in-95 duration-200 relative">
        <button onClick={() => onSwitchMode('customer')} className="absolute top-4 right-4 text-stone-400 hover:text-stone-800">
          <X size={20}/>
        </button>
        <div className="text-center mb-8">
          <div className="w-16 h-16 bg-rose-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <User size={32} className="text-rose-600" />
          </div>
          <h2 className="text-2xl font-serif font-bold text-stone-900">創作者工坊登入</h2>
          <p className="text-stone-500 text-sm mt-2">歡迎回來，繼續書寫您的故事</p>
        </div>
        
        <form onSubmit={handleSubmit} className="space-y-4">
          <div>
            <label className="block text-sm font-medium text-stone-700 mb-1">帳號 / 手機號碼</label>
            <input 
              type="text" 
              value={account}
              onChange={e => setAccount(e.target.value)}
              className="w-full p-3 border border-stone-300 rounded-lg focus:ring-2 focus:ring-rose-500 outline-none transition"
              placeholder="請輸入帳號"
            />
          </div>
          <div>
            <label className="block text-sm font-medium text-stone-700 mb-1">密碼</label>
            <input 
              type="password" 
              value={password}
              onChange={e => setPassword(e.target.value)}
              className="w-full p-3 border border-stone-300 rounded-lg focus:ring-2 focus:ring-rose-500 outline-none transition"
              placeholder="請輸入密碼"
            />
          </div>
          <button 
            type="submit" 
            disabled={isLoading}
            className="w-full bg-stone-900 text-white py-3 rounded-lg font-bold hover:bg-stone-800 transition flex items-center justify-center gap-2 active:scale-95"
          >
            {isLoading ? <Loader className="animate-spin" size={20}/> : '登入'}
          </button>
        </form>
        <div className="mt-6 text-center text-xs text-stone-400">
          <p className="mt-2">(測試帳號: creator / 任意密碼)</p>
        </div>
      </div>
    </div>
  );
};

// --- 元件：導覽列 ---
const Navbar = ({ currentMode, setMode, cartItems, onSearchClick, onCartClick, isSearchOpen, setSearchTerm, onMemberClick }) => {
  return (
    <>
    <nav className="sticky top-0 z-40 bg-stone-50/90 backdrop-blur-md border-b border-stone-200 transition-all">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex justify-between items-center h-16">
          <div className="flex items-center gap-4">
            <div 
              className="font-serif text-2xl font-bold text-rose-800 tracking-wider cursor-pointer select-none hover:opacity-80 transition"
              onClick={() => setMode('customer')}
            >
              HerStory
            </div>
            <div className="hidden md:flex bg-stone-200 rounded-full p-1 text-xs font-medium">
              <button 
                onClick={() => setMode('customer')}
                className={`px-3 py-1 rounded-full transition-all duration-300 ${currentMode === 'customer' ? 'bg-white shadow-sm text-stone-800' : 'text-stone-500 hover:text-stone-700'}`}
              >
                逛展覽
              </button>
              <button 
                onClick={() => setMode('creator')}
                className={`px-3 py-1 rounded-full transition-all duration-300 ${currentMode === 'creator' ? 'bg-rose-500 shadow-sm text-white' : 'text-stone-500 hover:text-stone-700'}`}
              >
                創作者後台
              </button>
              <button 
                onClick={() => setMode('b2b')}
                className={`px-3 py-1 rounded-full transition-all duration-300 ${currentMode === 'b2b' ? 'bg-emerald-600 shadow-sm text-white' : 'text-stone-500 hover:text-stone-700'}`}
              >
                企業合作
              </button>
            </div>
          </div>

          <div className="flex items-center space-x-4">
            {currentMode === 'customer' && (
              <>
                <button onClick={onSearchClick} className={`p-2 rounded-full transition active:scale-95 ${isSearchOpen ? 'bg-stone-200' : 'hover:bg-stone-200'}`}>
                  <Search className="w-5 h-5 text-stone-600" />
                </button>
                <button onClick={onCartClick} className="relative p-2 hover:bg-stone-200 rounded-full transition active:scale-95">
                  <ShoppingBag className="w-5 h-5 text-stone-600" />
                  {cartItems.length > 0 && (
                    <span className="absolute top-0 right-0 bg-rose-600 text-white text-[10px] w-4 h-4 flex items-center justify-center rounded-full animate-bounce">
                      {cartItems.length}
                    </span>
                  )}
                </button>
              </>
            )}
            <button className="p-2 hover:bg-stone-200 rounded-full transition active:scale-95" onClick={onMemberClick}>
              <User className="w-5 h-5 text-stone-600" />
            </button>
            <div className="md:hidden">
              <Menu className="w-6 h-6 text-stone-800" />
            </div>
          </div>
        </div>
      </div>
      
      {isSearchOpen && (
        <div className="bg-white border-b border-stone-200 animate-in slide-in-from-top-2 duration-200">
          <div className="max-w-7xl mx-auto px-4 py-3">
             <div className="relative">
                <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-stone-400 w-4 h-4" />
                <input 
                  type="text" 
                  placeholder="搜尋創作者、作品故事..." 
                  className="w-full bg-stone-100 pl-10 pr-4 py-2 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-rose-200"
                  autoFocus
                  onChange={(e) => setSearchTerm(e.target.value)}
                />
             </div>
             <div className="flex gap-2 mt-2 text-xs text-stone-500">
               <span>熱門搜尋：</span>
               <span className="cursor-pointer hover:text-rose-600" onClick={() => setSearchTerm('拼布')}>拼布</span>
               <span className="cursor-pointer hover:text-rose-600" onClick={() => setSearchTerm('藍染')}>藍染</span>
               <span className="cursor-pointer hover:text-rose-600" onClick={() => setSearchTerm('編織')}>編織</span>
             </div>
          </div>
        </div>
      )}

      <div className="md:hidden flex justify-around border-t border-stone-200 p-2 bg-stone-50 text-xs">
         <button onClick={() => setMode('customer')} className={`flex-1 py-2 text-center transition-colors ${currentMode === 'customer' ? 'text-rose-700 font-bold bg-white shadow-sm rounded-md' : 'text-stone-500'}`}>顧客</button>
         <button onClick={() => setMode('creator')} className={`flex-1 py-2 text-center transition-colors ${currentMode === 'creator' ? 'text-rose-700 font-bold bg-white shadow-sm rounded-md' : 'text-stone-500'}`}>創作者</button>
         <button onClick={() => setMode('b2b')} className={`flex-1 py-2 text-center transition-colors ${currentMode === 'b2b' ? 'text-emerald-700 font-bold bg-white shadow-sm rounded-md' : 'text-stone-500'}`}>企業</button>
      </div>
    </nav>
    </>
  );
};

// --- 新增元件：會員中心 ---
const MemberProfile = ({ onBack }) => {
  return (
    <div className="max-w-4xl mx-auto py-8 px-4 animate-in fade-in slide-in-from-bottom-5 duration-300">
      <button onClick={onBack} className="flex items-center text-stone-500 hover:text-stone-800 mb-6 transition-colors">
        <ChevronLeft size={20} /> 返回
      </button>
      <div className="flex items-center gap-4 mb-8">
        <div className="w-20 h-20 bg-stone-200 rounded-full flex items-center justify-center">
           <User size={40} className="text-stone-400"/>
        </div>
        <div>
           <h2 className="text-2xl font-bold text-stone-800">親愛的顧客</h2>
           <p className="text-stone-500">歡迎回到您的收藏空間</p>
        </div>
      </div>
      
      <div className="grid md:grid-cols-2 gap-8">
         <div className="bg-white p-6 rounded-xl shadow-sm border border-stone-100">
            <h3 className="font-bold text-lg mb-4 flex items-center gap-2"><ShoppingBag size={20} className="text-rose-600"/> 歷史訂單</h3>
            <div className="space-y-4">
              {MOCK_USER_ORDERS.map(order => (
                <div key={order.id} className="border-b pb-3 last:border-0">
                   <div className="flex justify-between items-center mb-1">
                      <span className="font-bold text-stone-700">{order.id}</span>
                      <span className="text-xs px-2 py-1 bg-green-100 text-green-700 rounded-full">{order.status}</span>
                   </div>
                   <p className="text-sm text-stone-500">{order.date} • {order.items.join(', ')}</p>
                   <p className="text-sm font-bold text-right mt-1">NT$ {order.total}</p>
                </div>
              ))}
            </div>
         </div>
         <div className="bg-white p-6 rounded-xl shadow-sm border border-stone-100">
            <h3 className="font-bold text-lg mb-4 flex items-center gap-2"><Heart size={20} className="text-rose-600"/> 收藏的故事</h3>
            <div className="text-center py-8 text-stone-400">
               <Heart size={48} className="mx-auto mb-2 opacity-20"/>
               <p>您還沒有收藏任何故事</p>
               <button onClick={onBack} className="text-rose-600 text-sm mt-2 hover:underline">去逛逛</button>
            </div>
         </div>
      </div>
    </div>
  );
};

// --- 新增元件：主題詳情頁 ---
const ThemeView = ({ theme, onBack }) => {
  if (!theme) return null;
  return (
    <div className="bg-stone-50 min-h-screen animate-in fade-in duration-500">
      <div className="relative h-[400px]">
        <img src={theme.img} className="w-full h-full object-cover" alt={theme.title}/>
        <div className="absolute inset-0 bg-black/50 flex flex-col items-center justify-center text-white p-4 text-center">
           <h1 className="text-5xl font-serif font-bold mb-4 tracking-widest">{theme.title}</h1>
           <p className="text-xl font-light opacity-90">{theme.desc}</p>
        </div>
        <button onClick={onBack} className="absolute top-8 left-8 text-white hover:opacity-70 flex items-center gap-2 bg-black/20 p-2 rounded-full backdrop-blur-sm">
           <ChevronLeft size={24}/>
        </button>
      </div>
      <div className="max-w-6xl mx-auto py-12 px-4">
         <div className="text-center mb-12">
            <h2 className="text-2xl font-serif font-bold text-stone-800 mb-2">精選作品</h2>
            <div className="w-16 h-1 bg-rose-600 mx-auto"></div>
         </div>
         <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
            {/* 模擬該主題下的作品，這裡重複使用 MOCK Data 來展示 */}
            {CREATORS.flatMap(c => c.products).slice(0, 3).map(product => (
               <div key={product.id} className="group cursor-pointer">
                  <div className="overflow-hidden aspect-square mb-3 relative rounded-sm">
                     <img src={product.image} alt={product.title} className="w-full h-full object-cover group-hover:scale-110 transition duration-500"/>
                  </div>
                  <h3 className="font-medium text-stone-900">{product.title}</h3>
                  <p className="text-stone-500 font-serif">NT$ {product.price}</p>
               </div>
            ))}
         </div>
         <div className="text-center mt-12">
            <p className="text-stone-500 italic">更多「{theme.title}」主題故事採集中...</p>
         </div>
      </div>
    </div>
  );
};

// --- 元件：創作者卡片與展示 ---
const CreatorCard = ({ creator, onClick }) => (
  <div 
    onClick={() => onClick(creator)}
    className="group cursor-pointer flex flex-col gap-3 bg-white p-4 pb-8 border border-stone-100 shadow-sm hover:shadow-xl transition-all duration-300 rounded-sm"
  >
    <div className="overflow-hidden aspect-[4/5] relative">
      <img 
        src={creator.heroImage} 
        alt={creator.name} 
        className="object-cover w-full h-full transform group-hover:scale-105 transition-transform duration-700 grayscale-[20%] group-hover:grayscale-0"
      />
      <div className="absolute bottom-0 left-0 w-full bg-gradient-to-t from-black/60 to-transparent p-4 pt-12">
         <h3 className="text-white font-serif text-xl tracking-wide">{creator.name}</h3>
         <p className="text-stone-200 text-sm">{creator.title}</p>
      </div>
    </div>
    <div className="flex gap-2 mt-2">
      {creator.tags.map(tag => (
        <span key={tag} className="text-xs px-2 py-1 bg-stone-100 text-stone-600 rounded-full">{tag}</span>
      ))}
    </div>
  </div>
);

const PodcastPlayer = ({ title, duration }) => {
  const [isPlaying, setIsPlaying] = useState(false);
  return (
    <div className="bg-stone-900 text-stone-50 p-4 rounded-lg flex items-center gap-4 shadow-lg my-6 select-none">
      <div 
        onClick={() => setIsPlaying(!isPlaying)}
        className="w-10 h-10 bg-rose-600 rounded-full flex items-center justify-center cursor-pointer hover:bg-rose-500 transition active:scale-95"
      >
        {isPlaying ? <Pause size={20} fill="white" /> : <Play size={20} fill="white" className="ml-1" />}
      </div>
      <div className="flex-1">
        <div className="flex justify-between items-end mb-1">
          <span className="text-sm font-medium tracking-wide">{title}</span>
          <span className="text-xs text-stone-400">{isPlaying ? "01:12 / " : ""}{duration}</span>
        </div>
        <div className="w-full bg-stone-700 h-1 rounded-full overflow-hidden">
          <div 
            className="bg-rose-500 h-full transition-all duration-500" 
            style={{ width: isPlaying ? '35%' : '0%' }}
          ></div>
        </div>
      </div>
      <div className="hidden sm:flex gap-1 items-end h-8">
        {[...Array(5)].map((_,i) => (
          <div key={i} className={`w-1 bg-rose-500/50 rounded-full ${isPlaying ? 'animate-pulse' : ''}`} style={{ height: `${30 + Math.random() * 70}%` }}></div>
        ))}
      </div>
    </div>
  );
};

const CreatorProfile = ({ creator, onBack, onAddToCart, onCommission, onNotify }) => {
  return (
    <div className="animate-in slide-in-from-right-10 duration-300 pb-20">
      <button onClick={onBack} className="flex items-center text-stone-500 hover:text-stone-800 mb-6 px-4 md:px-0 transition-colors">
        <ChevronLeft size={20} /> 返回策展牆
      </button>
      
      <div className="grid md:grid-cols-2 gap-12 items-start mb-16 px-4 md:px-0">
        <div className="relative group">
          <img src={creator.heroImage} alt={creator.name} className="w-full h-[300px] md:h-[500px] object-cover rounded-sm shadow-md transition group-hover:shadow-xl" />
          <div className="absolute -bottom-6 -right-6 w-24 h-24 md:w-32 md:h-32 border-4 border-stone-50 rounded-full overflow-hidden shadow-xl">
            <img src={creator.avatar} alt="avatar" className="w-full h-full object-cover" />
          </div>
        </div>
        
        <div>
          <h1 className="text-4xl font-serif font-bold text-stone-900 mb-2">{creator.name}</h1>
          <p className="text-lg text-rose-700 font-medium mb-6">{creator.title}</p>
          
          <PodcastPlayer title={creator.audioTitle} duration={creator.audioDuration} />
          
          <div className="prose prose-stone text-stone-600 leading-relaxed mb-8">
            <p>{creator.story}</p>
          </div>
          
          <button 
            onClick={onCommission}
            className="w-full md:w-auto bg-stone-900 text-white px-8 py-4 rounded-sm hover:bg-stone-800 transition active:scale-95 flex items-center justify-center gap-2 shadow-lg hover:shadow-xl"
          >
            <Sparkles size={18} />
            我很喜歡這個風格，我想客製化
          </button>
        </div>
      </div>

      <div className="px-4 md:px-0">
        <h2 className="text-2xl font-serif font-bold text-stone-900 mb-8 border-l-4 border-rose-600 pl-4">作品展間</h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {creator.products.map(product => (
            <div key={product.id} className="group cursor-pointer">
              <div className="overflow-hidden aspect-square mb-3 relative rounded-sm">
                <img src={product.image} alt={product.title} className="w-full h-full object-cover group-hover:scale-110 transition duration-500" />
                <button 
                  onClick={(e) => {
                     e.stopPropagation();
                     onAddToCart(product);
                     onNotify(`已將 ${product.title} 加入收藏`);
                  }}
                  className="absolute bottom-3 right-3 bg-white hover:bg-rose-600 hover:text-white text-stone-800 p-2 rounded-full shadow-md transition active:scale-95"
                >
                   <ShoppingBag size={18} />
                </button>
                <div className="absolute top-3 right-3 bg-white/80 p-2 rounded-full opacity-0 group-hover:opacity-100 transition">
                  <Heart size={18} className="text-stone-600 hover:text-rose-600" />
                </div>
              </div>
              <h3 className="font-medium text-stone-900 group-hover:text-rose-700 transition">{product.title}</h3>
              <p className="text-stone-500 font-serif">NT$ {product.price}</p>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

const CustomerView = ({ currentView, setCurrentView, selectedCreator, setSelectedCreator, addToCart, searchTerm, onNotify, selectedTheme, setSelectedTheme }) => {
  const [isCommissionModalOpen, setCommissionModalOpen] = useState(false);

  const handleCommissionSubmit = (e) => {
    e.preventDefault();
    onNotify("您的客製化需求已發送！創作者將盡快回覆。");
    setCommissionModalOpen(false);
  };

  const filteredCreators = CREATORS.filter(c => 
    c.name.includes(searchTerm) || 
    c.story.includes(searchTerm) || 
    c.tags.some(t => t.includes(searchTerm))
  );

  if (currentView === 'profile' && selectedCreator) {
    return (
      <div className="max-w-6xl mx-auto py-8">
        <CreatorProfile 
          creator={selectedCreator} 
          onBack={() => setCurrentView('home')} 
          onAddToCart={addToCart}
          onCommission={() => setCommissionModalOpen(true)}
          onNotify={onNotify}
        />
        
        <Modal isOpen={isCommissionModalOpen} onClose={() => setCommissionModalOpen(false)} title={`向 ${selectedCreator.name} 提出客製化需求`}>
           <form onSubmit={handleCommissionSubmit} className="space-y-4">
             <div>
               <label className="block text-sm font-bold text-stone-700 mb-1">您想客製化什麼？</label>
               <select className="w-full p-2 border rounded-md">
                 <option>調整現有作品尺寸</option>
                 <option>更換花色/布料</option>
                 <option>全新設計委託</option>
               </select>
             </div>
             <div>
               <label className="block text-sm font-bold text-stone-700 mb-1">需求描述</label>
               <textarea className="w-full p-2 border rounded-md h-24" placeholder="例如：我想要一個適合放 13 吋筆電的拼布包，偏好藍色系..."></textarea>
             </div>
             <div className="bg-rose-50 p-3 rounded-md text-sm text-rose-800 flex items-start gap-2">
               <Sparkles size={16} className="mt-1 flex-shrink-0" />
               <p>AI 小提示：您可以上傳參考圖片，能幫助創作者更準確理解您的想法喔！</p>
             </div>
             <button type="submit" className="w-full bg-stone-900 text-white py-3 rounded-md font-bold hover:bg-stone-800 transition active:scale-95">發送需求</button>
           </form>
        </Modal>

        <AiChatBot type="customer" onNotify={onNotify} />
      </div>
    );
  }

  if (currentView === 'theme' && selectedTheme) {
      return <ThemeView theme={selectedTheme} onBack={() => setCurrentView('home')} />
  }

  return (
    <div>
      <header className="relative h-[80vh] flex items-center justify-center overflow-hidden">
        <img 
          src="https://images.unsplash.com/photo-1512403754473-27835f7b9984?auto=format&fit=crop&q=80&w=1600&h=900" 
          className="absolute inset-0 w-full h-full object-cover opacity-90 transition-transform duration-[20s] hover:scale-105"
          alt="Art Gallery Atmosphere"
        />
        <div className="absolute inset-0 bg-stone-900/30"></div>
        <div className="relative z-10 text-center text-white px-4 animate-in fade-in zoom-in duration-1000">
          <p className="text-lg md:text-xl font-light tracking-[0.3em] mb-4 text-stone-100">STORY-BASED CURATION</p>
          <h1 className="text-5xl md:text-7xl font-serif font-bold mb-6 tracking-wide leading-tight drop-shadow-md">
            每一件作品<br/>都是一段人生故事
          </h1>
          <button 
            onClick={() => document.getElementById('curation-wall').scrollIntoView({behavior: 'smooth'})}
            className="mt-8 px-8 py-3 border border-white hover:bg-white hover:text-stone-900 transition text-sm tracking-widest uppercase backdrop-blur-sm"
          >
            探索本週策展
          </button>
        </div>
      </header>

      <section id="curation-wall" className="max-w-7xl mx-auto py-20 px-4 md:px-8">
        <div className="flex justify-between items-end mb-12">
          <div>
            <h2 className="text-3xl font-serif font-bold text-stone-900 mb-2">遇見創作者</h2>
            <p className="text-stone-500">聆聽她們的生命故事，收藏獨一無二的手作溫度</p>
          </div>
          <button className="text-rose-700 border-b border-rose-700 pb-1 hover:opacity-70 hidden md:block" onClick={() => {
              setCurrentView('home');
              window.scrollTo({top: document.getElementById('curation-wall').offsetTop, behavior: 'smooth'});
              onNotify("更多精彩創作者，每週五更新");
          }}>查看所有創作者</button>
        </div>

        {filteredCreators.length > 0 ? (
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            {filteredCreators.map(creator => (
              <CreatorCard 
                key={creator.id} 
                creator={creator} 
                onClick={(c) => {
                  setSelectedCreator(c);
                  setCurrentView('profile');
                }} 
              />
            ))}
            <div className="bg-stone-100 flex items-center justify-center flex-col p-8 text-center text-stone-400 border border-dashed border-stone-300 rounded-sm min-h-[400px]">
              <span className="mb-2 font-serif text-lg">更多故事正在編織中</span>
              <span className="text-xs tracking-wider">Coming Soon</span>
            </div>
          </div>
        ) : (
          <div className="text-center py-20 bg-stone-50 rounded-lg">
            <p className="text-stone-500 text-lg">找不到符合「{searchTerm}」的創作者...</p>
            <button onClick={() => window.scrollTo(0, 0)} className="text-rose-600 mt-2 hover:underline">清除搜尋</button>
          </div>
        )}
      </section>

      <section className="bg-stone-100 py-20 px-4">
        <div className="max-w-7xl mx-auto">
          <h2 className="text-3xl font-serif font-bold text-stone-900 mb-12 text-center">主題展間</h2>
          <div className="grid grid-cols-1 md:grid-cols-3 gap-4 h-[500px]">
            {THEMES.map((theme) => (
              <div key={theme.id} className="relative group overflow-hidden cursor-pointer h-64 md:h-auto" onClick={() => {
                  setSelectedTheme(theme);
                  setCurrentView('theme');
              }}>
                <img src={theme.img} className="w-full h-full object-cover transition duration-700 group-hover:scale-110" alt={theme.title} />
                <div className="absolute inset-0 bg-black/40 group-hover:bg-black/20 transition flex items-center justify-center">
                  <span className="text-white text-2xl font-serif tracking-widest border border-white px-6 py-2">{theme.title}</span>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>
      
      <AiChatBot type="customer" onNotify={onNotify} />
    </div>
  );
};

// --- 創作者端 (Creator Side) ---
const CreatorDashboard = ({ onLogout, onNotify }) => {
  const [view, setView] = useState('home'); // home, upload, orders
  const [uploadStep, setUploadStep] = useState(1);
  const [isAiProcessing, setIsAiProcessing] = useState(false);
  const [activeModal, setActiveModal] = useState(null); // 'mission', 'tips', 'orderDetail'
  const [selectedOrder, setSelectedOrder] = useState(null);

  const [productData, setProductData] = useState({
    image: null, material: '', timeSpent: '', mood: '', aiCopy: '', aiStory: '', priceBreakdown: { material: 0, labor: 0, premium: 0, total: 0 }
  });

  const handleAiGeneration = () => {
    if (!productData.image) { onNotify("請先上傳一張作品照片！", "error"); return; }
    setIsAiProcessing(true);
    setTimeout(() => {
      setProductData(prev => ({
        ...prev,
        aiCopy: `這款${prev.material}手作包，不僅承載了${prev.timeSpent}小時的專注與溫度，更融合了傳統技藝與現代美學。每一個繩結都是對生活的祝福，堅韌而溫柔。`,
        aiStory: `創作這件作品的那天，陽光正好灑在窗前的舊布料上。我想起小時候看著母親縫糢的背影，那種單純想為家人做點什麼的心情，就是這款作品的靈魂。這不只是一個包，這是一份溫暖的陪伴。`,
        priceBreakdown: { material: 350, labor: 800, premium: 400, total: 1550 }
      }));
      setIsAiProcessing(false);
      setUploadStep(3);
    }, 2500);
  };

  const handleImageUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => setProductData({...productData, image: reader.result});
      reader.readAsDataURL(file);
    }
  };

  if (view === 'orders') {
    return (
      <div className="bg-stone-50 min-h-screen p-4 md:p-8 pb-20 animate-in slide-in-from-right-10 duration-200">
         <div className="max-w-4xl mx-auto">
            <button onClick={() => setView('home')} className="flex items-center text-stone-500 mb-6 hover:text-stone-800"><ChevronLeft size={20}/> 返回工作台</button>
            <h1 className="text-2xl font-bold mb-6">訂單管理</h1>
            <div className="bg-white rounded-xl shadow-sm overflow-hidden">
               {MOCK_ORDERS.map((order) => (
                 <div key={order.id} className="p-4 border-b last:border-0 flex justify-between items-center hover:bg-stone-50 transition cursor-pointer" onClick={() => { setSelectedOrder(order); setActiveModal('orderDetail'); }}>
                    <div>
                      <div className="flex items-center gap-2 mb-1">
                        <span className="font-bold text-stone-800">{order.id}</span>
                        <span className={`text-xs px-2 py-0.5 rounded-full ${order.status === '待確認' ? 'bg-rose-100 text-rose-700' : 'bg-emerald-100 text-emerald-700'}`}>{order.status}</span>
                      </div>
                      <p className="text-stone-600 text-sm">{order.item} - {order.buyer}</p>
                    </div>
                    <div className="text-right">
                       <span className="text-xs text-stone-400 block">{order.date}</span>
                       <ChevronLeft className="rotate-180 text-stone-300 w-5 h-5 ml-auto mt-1" />
                    </div>
                 </div>
               ))}
            </div>
         </div>
         <AiChatBot type="creator" onNotify={onNotify} />
         
         <Modal isOpen={activeModal === 'orderDetail' && selectedOrder} onClose={() => setActiveModal(null)} title={`訂單詳情 ${selectedOrder?.id}`}>
            <div className="space-y-4">
               <div className="flex justify-between border-b pb-2">
                 <span className="text-stone-500">商品</span>
                 <span className="font-bold">{selectedOrder?.item}</span>
               </div>
               <div className="flex justify-between border-b pb-2">
                 <span className="text-stone-500">買家</span>
                 <span>{selectedOrder?.buyer}</span>
               </div>
               <div className="bg-stone-50 p-3 rounded-lg">
                 <span className="text-xs text-stone-400 block mb-1">客製化需求備註</span>
                 <p className="text-stone-800">{selectedOrder?.details}</p>
               </div>
               <div className="flex justify-between items-center pt-2">
                 <span className="font-bold text-lg">總金額</span>
                 <span className="font-bold text-lg text-rose-600">NT$ {selectedOrder?.price}</span>
               </div>
               <div className="flex gap-2 pt-4">
                 <button className="flex-1 bg-stone-200 text-stone-800 py-2 rounded-lg hover:bg-stone-300" onClick={() => setActiveModal(null)}>關閉</button>
                 <button className="flex-1 bg-rose-600 text-white py-2 rounded-lg hover:bg-rose-700" onClick={() => { onNotify("已通知買家開始製作！"); setActiveModal(null); }}>接單製作</button>
               </div>
            </div>
         </Modal>
      </div>
    );
  }

  if (view === 'upload') {
    return (
    <div className="bg-stone-50 min-h-screen pb-20 animate-in slide-in-from-right-10 duration-200">
      <div className="bg-white p-4 shadow-sm sticky top-0 z-40 flex items-center gap-4">
        <button onClick={() => setView('home')}><ChevronLeft /></button>
        <h2 className="font-bold text-lg">上架新作品</h2>
      </div>
      <div className="max-w-2xl mx-auto p-4 md:p-8">
        <div className="flex items-center justify-between mb-8 px-8">
          {[1, 2, 3].map(step => (
            <React.Fragment key={step}>
              <div className={`w-8 h-8 rounded-full flex items-center justify-center transition-colors duration-500 ${uploadStep >= step ? 'bg-rose-600 text-white' : 'bg-stone-200'}`}>{step}</div>
              {step < 3 && <div className={`flex-1 h-1 mx-2 transition-colors duration-500 ${uploadStep > step ? 'bg-rose-600' : 'bg-stone-200'}`}></div>}
            </React.Fragment>
          ))}
        </div>

        {uploadStep === 1 && (
          <div className="animate-in fade-in slide-in-from-bottom-5 duration-300 space-y-6">
            <div className="bg-white p-6 rounded-xl shadow-sm text-center border-2 border-dashed border-stone-300 hover:border-rose-400 cursor-pointer relative h-64 flex flex-col items-center justify-center group transition">
               <input type="file" onChange={handleImageUpload} className="absolute inset-0 w-full h-full opacity-0 cursor-pointer" accept="image/*" />
               {productData.image ? <img src={productData.image} alt="Preview" className="h-full object-contain" /> : <><ImageIcon size={48} className="text-stone-300 mb-2 group-hover:text-rose-400" /><p className="text-stone-500 font-medium">點擊拍照或上傳圖片</p></>}
            </div>
            <div className="space-y-4">
              {['主要材料是什麼？', '大概花了多久製作？(小時)'].map((label, i) => (
                <div key={i}>
                  <label className="block text-sm font-bold text-stone-700 mb-1">{label}</label>
                  <input type={i===1?"number":"text"} className="w-full p-3 border border-stone-300 rounded-lg focus:ring-2 focus:ring-rose-500 outline-none" 
                    value={i===0 ? productData.material : productData.timeSpent}
                    onChange={(e) => setProductData(prev => ({...prev, [i===0?'material':'timeSpent']: e.target.value}))}
                  />
                </div>
              ))}
            </div>
            <button onClick={() => setUploadStep(2)} className="w-full bg-rose-600 text-white py-4 rounded-xl font-bold text-lg shadow-md hover:bg-rose-700 transition active:scale-95">下一步：呼叫 AI 小幫手</button>
          </div>
        )}

        {uploadStep === 2 && (
          <div className="flex flex-col items-center justify-center py-12 text-center animate-in fade-in slide-in-from-bottom-5 duration-300">
            {isAiProcessing ? (
               <><div className="w-20 h-20 bg-rose-100 rounded-full flex items-center justify-center mb-6 relative"><Sparkles size={40} className="text-rose-500 animate-spin-slow" /></div><h3 className="text-xl font-bold text-stone-800 mb-2">AI 正在品味您的作品...</h3></>
            ) : (
               <div className="w-full">
                  <div className="bg-gradient-to-br from-indigo-500 to-purple-600 text-white p-8 rounded-2xl mb-8 shadow-xl"><Sparkles size={48} className="mb-4 mx-auto text-yellow-300" /><h2 className="text-2xl font-bold mb-2">魔法準備好了！</h2><p>我會幫您寫好文案，並建議一個合理的價格。</p></div>
                  <button onClick={handleAiGeneration} className="w-full bg-stone-900 text-white py-4 rounded-xl font-bold text-lg shadow-md hover:bg-stone-800 transition flex items-center justify-center gap-2 active:scale-95"><Sparkles size={20} /> 開始生成</button>
               </div>
            )}
          </div>
        )}

        {uploadStep === 3 && (
          <div className="animate-in fade-in slide-in-from-bottom-5 duration-300 space-y-6">
            <div className="bg-white p-6 rounded-xl shadow-sm border border-stone-200">
              <h3 className="font-bold text-lg flex items-center gap-2 mb-4"><Edit3 size={18} className="text-rose-500" /> AI 故事文案</h3>
              <div className="space-y-4">
                <div className="p-4 bg-stone-50 rounded-lg"><label className="text-xs text-stone-400 block mb-1">產品敘述</label><p className="text-stone-700 text-sm">{productData.aiCopy}</p></div>
                <div className="p-4 bg-orange-50 rounded-lg"><label className="text-xs text-orange-400 block mb-1">情感故事 (亮點)</label><p className="text-stone-700 text-sm italic">"{productData.aiStory}"</p></div>
              </div>
            </div>
            <div className="bg-white p-6 rounded-xl shadow-sm border border-stone-200">
               <h3 className="font-bold text-lg flex items-center gap-2 mb-4"><DollarSign size={18} className="text-emerald-500" /> AI 定價建議</h3>
               <div className="text-center mb-6"><span className="text-4xl font-bold text-stone-900">NT$ {productData.priceBreakdown.total}</span></div>
               <div className="space-y-2 text-sm text-stone-500 bg-stone-50 p-4 rounded-lg">
                 <div className="flex justify-between"><span>工時價值</span><span>${productData.priceBreakdown.labor}</span></div>
                 <div className="flex justify-between text-rose-600 font-bold"><span>獨家設計溢價</span><span>+ ${productData.priceBreakdown.premium}</span></div>
               </div>
            </div>
            <button onClick={() => { onNotify("恭喜！作品已成功上架！"); setView('home'); }} className="w-full bg-stone-900 text-white py-4 rounded-xl font-bold text-lg shadow-md hover:bg-stone-800 transition active:scale-95">確認發布 (上架)</button>
          </div>
        )}
      </div>
      <AiChatBot type="creator" onNotify={onNotify} />
    </div>
    );
  }

  return (
    <div className="bg-stone-50 min-h-screen p-4 md:p-8 relative">
      <div className="max-w-4xl mx-auto">
        <div className="flex justify-between items-center mb-8">
          <div><h1 className="text-2xl font-bold text-stone-800">早安，秀琴姐！☀️</h1><p className="text-stone-500">今天也是充滿靈感的一天</p></div>
          <div className="flex gap-4 items-center">
             <img src={CREATORS[0].avatar} className="w-12 h-12 rounded-full shadow-sm" alt="profile" />
             <button onClick={onLogout} className="bg-white p-2 rounded-full text-stone-400 hover:text-red-600 shadow-sm transition"><LogOut size={20}/></button>
          </div>
        </div>

        <div className="bg-gradient-to-r from-rose-500 to-orange-400 rounded-xl p-6 text-white shadow-lg mb-8 relative overflow-hidden group cursor-pointer hover:shadow-2xl transition" onClick={() => setActiveModal('mission')}>
          <div className="relative z-10">
            <div className="flex justify-between items-start mb-4">
              <div><h2 className="text-xl font-bold mb-1">本月賦能任務</h2><p className="text-rose-100 text-sm">再上傳 1 件作品，即可解鎖免費 Podcast 工作坊！</p></div>
              <div className="bg-white/20 p-2 rounded-lg"><Mic size={24} /></div>
            </div>
            <div className="w-full bg-black/20 h-3 rounded-full overflow-hidden"><div className="bg-white h-full w-4/5"></div></div>
            <div className="text-right text-xs mt-1 font-mono">進度 4/5</div>
          </div>
          <div className="absolute -right-10 -bottom-10 w-40 h-40 bg-white/10 rounded-full group-hover:scale-110 transition duration-500"></div>
        </div>

        <div className="grid grid-cols-2 gap-4 mb-8">
          <button onClick={() => { setView('upload'); setUploadStep(1); }} className="bg-white p-6 rounded-xl shadow-sm hover:shadow-md transition flex flex-col items-center justify-center gap-3 border-2 border-transparent hover:border-rose-500 group active:scale-95">
            <div className="w-16 h-16 bg-rose-100 rounded-full flex items-center justify-center group-hover:bg-rose-500 transition"><Camera size={32} className="text-rose-600 group-hover:text-white" /></div>
            <span className="font-bold text-stone-700 text-lg">上傳新作品</span>
          </button>
          <button onClick={() => setView('orders')} className="bg-white p-6 rounded-xl shadow-sm hover:shadow-md transition flex flex-col items-center justify-center gap-3 border-2 border-transparent hover:border-emerald-500 group active:scale-95">
            <div className="w-16 h-16 bg-emerald-100 rounded-full flex items-center justify-center group-hover:bg-emerald-500 transition"><CheckCircle size={32} className="text-emerald-600 group-hover:text-white" /></div>
            <span className="font-bold text-stone-700 text-lg">查看訂單 (2)</span>
          </button>
        </div>
        
        <div className="bg-white p-6 rounded-xl shadow-sm cursor-pointer hover:bg-yellow-50 transition border border-transparent hover:border-yellow-200" onClick={() => setActiveModal('tips')}>
          <h3 className="font-bold text-stone-700 mb-4">小幫手提示</h3>
          <div className="flex gap-4 items-start">
            <div className="bg-yellow-100 p-2 rounded-full"><Sparkles size={20} className="text-yellow-600"/></div>
            <p className="text-stone-600 text-sm">昨天有顧客詢問是否可以客製化「藍色系的拼布包」，建議您可以拍一些藍色布料的照片上傳到動態喔！</p>
          </div>
        </div>
      </div>
      <AiChatBot type="creator" onNotify={onNotify} />

      <Modal isOpen={activeModal === 'mission'} onClose={() => setActiveModal(null)} title="賦能任務詳情">
         <div className="text-center">
            <div className="w-20 h-20 bg-rose-100 rounded-full flex items-center justify-center mx-auto mb-4"><Mic size={40} className="text-rose-600" /></div>
            <h3 className="font-bold text-lg mb-2">Podcast 故事行銷工作坊</h3>
            <p className="text-stone-500 text-sm mb-4">學會用聲音記錄您的創作故事，讓更多人聽見您的心聲。完成本月任務即可免費參加 (市價 $2,000)。</p>
            <div className="bg-stone-100 rounded-lg p-3 text-sm text-left mb-6">
               <div className="flex justify-between mb-1"><span>上架 5 件作品</span><span>4/5</span></div>
               <div className="w-full bg-stone-300 h-2 rounded-full overflow-hidden"><div className="bg-rose-500 w-4/5 h-full"></div></div>
            </div>
            <button className="w-full bg-rose-600 text-white py-2 rounded-lg" onClick={() => { setActiveModal(null); setView('upload'); }}>去完成任務 (上架作品)</button>
         </div>
      </Modal>

      <Modal isOpen={activeModal === 'tips'} onClose={() => setActiveModal(null)} title="市場洞察提示">
         <div className="space-y-4">
            <div className="flex gap-3">
               <div className="bg-blue-100 p-2 rounded-full h-fit"><Search size={20} className="text-blue-600"/></div>
               <div>
                  <h4 className="font-bold text-stone-800">藍色系商品搜尋量上升 150%</h4>
                  <p className="text-sm text-stone-500">隨著夏天接近，顧客開始尋找清爽的視覺色系。</p>
               </div>
            </div>
            <hr />
            <div className="bg-yellow-50 p-4 rounded-lg">
               <h4 className="font-bold text-yellow-800 mb-2">建議行動：</h4>
               <ul className="list-disc pl-5 text-sm text-yellow-800 space-y-1">
                  <li>整理手邊的藍染布料</li>
                  <li>拍攝自然光下的藍色系作品</li>
                  <li>上架時加上 #夏日藍染 標籤</li>
               </ul>
            </div>
            <button className="w-full bg-stone-900 text-white py-2 rounded-lg" onClick={() => setActiveModal(null)}>收到，謝謝小幫手！</button>
         </div>
      </Modal>
    </div>
  );
};

// --- B2B 企業專區 (B2B Zone) ---
const B2BPage = ({ onNotify }) => {
  const [isFormOpen, setIsFormOpen] = useState(false);
  const handleSubmit = (e) => {
    e.preventDefault();
    onNotify("感謝您的詢問！我們的專案經理將盡快聯繫您。");
    setIsFormOpen(false);
  }

  return (
  <div className="bg-white min-h-screen pb-20">
    <div className="bg-emerald-900 text-white py-20 px-8 text-center relative overflow-hidden">
      <div className="absolute top-0 left-0 w-32 h-32 bg-white/10 rounded-full blur-3xl"></div>
      <img src="https://images.unsplash.com/photo-1556761175-5973dc0f32e7?auto=format&fit=crop&q=80&w=1600&h=600" className="absolute inset-0 w-full h-full object-cover opacity-20" alt="B2B Meeting" />
      <div className="relative z-10 max-w-4xl mx-auto animate-in fade-in slide-in-from-bottom-5 duration-700">
        <span className="text-emerald-300 tracking-widest text-sm font-bold uppercase mb-4 block">CSR / ESG Solution</span>
        <h1 className="text-4xl md:text-5xl font-bold mb-6 font-serif">讓企業採購更有溫度與影響力</h1>
        <p className="text-emerald-100 text-lg mb-8 max-w-2xl mx-auto">您的每一次採購，都在支持一位婦女的經濟獨立，實現真正的社會共融。</p>
        <button onClick={() => setIsFormOpen(true)} className="bg-white text-emerald-900 px-8 py-3 rounded-sm font-bold hover:bg-emerald-50 transition hover:shadow-lg transform hover:-translate-y-1 active:scale-95">提交採購需求</button>
      </div>
    </div>
    
    <div className="max-w-7xl mx-auto py-16 px-4 grid md:grid-cols-3 gap-8">
      {[
        {icon:Briefcase, t:'企業禮贈品', d:'不再是冰冷的工廠製品。提供具故事性、手工溫度的節慶禮盒。'},
        {icon:User, t:'員工制服/配件', d:'結合再生布料與獨特設計，展現企業永續形象的穿搭。'},
        {icon:Globe, t:'ESG 影響力報告', d:'我們會為您計算採購創造的「社會影響力數據」，納入您的 CSR 報告書。'}
      ].map((item, i) => (
         <div key={i} className="p-8 border border-stone-200 rounded-lg text-center hover:shadow-lg transition cursor-pointer hover:border-emerald-500 group">
           <item.icon size={40} className="mx-auto text-emerald-700 mb-4 group-hover:scale-110 transition" />
           <h3 className="font-bold text-xl mb-2">{item.t}</h3>
           <p className="text-stone-500">{item.d}</p>
         </div>
      ))}
    </div>

    <Modal isOpen={isFormOpen} onClose={() => setIsFormOpen(false)} title="企業採購諮詢">
      <form onSubmit={handleSubmit} className="space-y-4">
        <div><label className="block text-sm font-bold mb-1">企業名稱</label><input required type="text" className="w-full p-2 border rounded" placeholder="例如：織光科技股份有限公司"/></div>
        <div><label className="block text-sm font-bold mb-1">聯絡人</label><input required type="text" className="w-full p-2 border rounded" placeholder="例如：王經理"/></div>
        <div><label className="block text-sm font-bold mb-1">預計採購項目</label>
           <select className="w-full p-2 border rounded">
              <option>節慶禮盒 (50份以上)</option>
              <option>員工制服/配件</option>
              <option>活動周邊紀念品</option>
              <option>長期公益合作</option>
           </select>
        </div>
        <div><label className="block text-sm font-bold mb-1">需求簡述</label><textarea className="w-full p-2 border rounded h-24" placeholder="請簡述您的預算範圍與期望..."></textarea></div>
        <button type="submit" className="w-full bg-emerald-700 text-white py-3 rounded font-bold hover:bg-emerald-800">送出諮詢單</button>
      </form>
    </Modal>
  </div>
  );
};

// --- 共用元件：結帳彈窗 ---
const CheckoutModal = ({ isOpen, onClose, total, onConfirm }) => {
   const [step, setStep] = useState(1);
   const [loading, setLoading] = useState(false);

   const handlePay = () => {
      setLoading(true);
      setTimeout(() => {
         setLoading(false);
         setStep(2); // Success step
      }, 1500);
   };

   if (!isOpen) return null;

   return (
      <div className="fixed inset-0 z-[60] flex items-center justify-center bg-black/50 backdrop-blur-sm p-4 animate-in fade-in">
         <div className="bg-white rounded-xl shadow-2xl w-full max-w-md overflow-hidden relative">
            <button onClick={onClose} className="absolute top-4 right-4 p-1 hover:bg-stone-100 rounded-full z-10"><X size={20}/></button>
            
            {step === 1 ? (
               <div className="p-6">
                  <h3 className="font-bold text-xl mb-6 flex items-center gap-2"><CreditCard /> 結帳資訊</h3>
                  <div className="space-y-4 mb-6">
                     <div><label className="block text-sm font-bold mb-1">收件人姓名</label><input type="text" className="w-full p-2 border rounded" placeholder="請輸入姓名"/></div>
                     <div><label className="block text-sm font-bold mb-1">聯絡電話</label><input type="text" className="w-full p-2 border rounded" placeholder="09xx-xxx-xxx"/></div>
                     <div><label className="block text-sm font-bold mb-1">付款方式</label>
                        <select className="w-full p-2 border rounded">
                           <option>信用卡 (VISA/Master)</option>
                           <option>LINE Pay</option>
                           <option>貨到付款</option>
                        </select>
                     </div>
                     <div className="bg-stone-50 p-4 rounded-lg flex justify-between items-center">
                        <span className="font-bold text-stone-600">應付金額</span>
                        <span className="font-bold text-xl text-rose-600">NT$ {total}</span>
                     </div>
                  </div>
                  <button onClick={handlePay} disabled={loading} className="w-full bg-stone-900 text-white py-3 rounded font-bold hover:bg-stone-800 flex justify-center gap-2">
                     {loading ? <Loader className="animate-spin"/> : '確認付款'}
                  </button>
               </div>
            ) : (
               <div className="p-8 text-center bg-stone-50">
                  <div className="w-16 h-16 bg-green-100 text-green-600 rounded-full flex items-center justify-center mx-auto mb-4 animate-in zoom-in">
                     <CheckCircle size={32} />
                  </div>
                  <h3 className="font-bold text-2xl mb-2">訂購成功！</h3>
                  <p className="text-stone-500 mb-6">感謝您的支持，創作者將盡快為您製作。</p>
                  <button onClick={() => { onConfirm(); onClose(); setStep(1); }} className="w-full bg-stone-900 text-white py-3 rounded font-bold">
                     繼續逛逛
                  </button>
               </div>
            )}
         </div>
      </div>
   );
};

// --- 共用元件：加入創作者彈窗 ---
const JoinCreatorModal = ({ isOpen, onClose, onNotify }) => {
    const handleSubmit = (e) => {
        e.preventDefault();
        onNotify("申請已送出！我們將在3個工作天內審核");
        onClose();
    };

    if (!isOpen) return null;
    return (
        <Modal isOpen={isOpen} onClose={onClose} title="成為創作者">
            <form onSubmit={handleSubmit} className="space-y-4">
                <div className="bg-rose-50 p-4 rounded-lg text-sm text-rose-800 mb-4">
                    <p>加入 HerStory，您將獲得：</p>
                    <ul className="list-disc pl-5 mt-2 space-y-1">
                        <li>專屬作品展示空間</li>
                        <li>AI 文案與定價小幫手</li>
                        <li>免費的故事行銷工作坊</li>
                    </ul>
                </div>
                <div><label className="block text-sm font-bold mb-1">品牌名稱</label><input required className="w-full p-2 border rounded"/></div>
                <div><label className="block text-sm font-bold mb-1">創作類型</label><input required className="w-full p-2 border rounded" placeholder="例如：拼布、陶藝..."/></div>
                <div><label className="block text-sm font-bold mb-1">作品集連結 (IG/FB)</label><input className="w-full p-2 border rounded"/></div>
                <button type="submit" className="w-full bg-stone-900 text-white py-3 rounded font-bold hover:bg-stone-800">送出申請</button>
            </form>
        </Modal>
    );
};

// --- 主程式 (App) ---
const App = () => {
  const [currentMode, setMode] = useState('customer');
  const [currentView, setCurrentView] = useState('home');
  const [selectedCreator, setSelectedCreator] = useState(null);
  const [selectedTheme, setSelectedTheme] = useState(null);
  const [cartItems, setCartItems] = useState([
     { id: 101, title: "昭和風再生拼布包", price: 1280, image: "https://images.unsplash.com/photo-1590874103328-eac38a683ce7?auto=format&fit=crop&q=80&w=200&h=200" },
     { id: 102, title: "手作藍染杯墊組", price: 450, image: "https://cms-artifacts.artlist.io/content/generated-image-v1/image__5/generated-image-02895c87-b4b5-4ef5-8714-9c1eca59e81b.png?Expires=2080480487&Key-Pair-Id=K2ZDLYDZI2R1DF&Signature=UqhH4Ab0dCk-Il94nAXMZq3VX-Z3RgeBI~dWqwDsuW81TQw3UcLd-GaD-iwOx3QQBewfML585Onu2oMbCWd-6mpO2NjFzp8xWs9GGNHb3KYtlYiCwuSj7RYZvCxkTcKdI38n3vTMiTKA2sO441-jT-k9BGgj~0LiNzP9jEM~bhUuym-gSijT8WBFG8iFuajlyAelvx3dk734gBtnUXzkF~9gTk45NncK01ocm1Qqf5Cj3IW4O9Y0fcII99pVnsRM91TRfrolhMbq4n8RrmNG01AcyWn4uuPk6kGoOH01gksuD9Rd~AbxzIUhZqXvC-rTRlPVkIdKuJLdzWQLudnrXw__" }
  ]);
  const [creatorUser, setCreatorUser] = useState(null);
  
  // States for UI
  const [isSearchOpen, setIsSearchOpen] = useState(false);
  const [isCartOpen, setIsCartOpen] = useState(false);
  const [searchTerm, setSearchTerm] = useState('');
  const [notification, setNotification] = useState(null);
  const [isCheckoutOpen, setIsCheckoutOpen] = useState(false);
  const [isJoinModalOpen, setIsJoinModalOpen] = useState(false);

  // Helper Functions
  const showNotification = (message, type = 'success') => {
      setNotification({ message, type });
  };

  const handleAddToCart = (product) => {
    setCartItems([...cartItems, product]);
    setIsCartOpen(true);
  };

  const handleRemoveFromCart = (index) => {
    const newItems = [...cartItems];
    newItems.splice(index, 1);
    setCartItems(newItems);
  };

  const cartTotal = cartItems.reduce((sum, item) => sum + item.price, 0);

  const handleModeSwitch = (mode) => {
    setMode(mode);
    setCurrentView('home');
    setIsSearchOpen(false);
    setIsCartOpen(false);
    window.scrollTo(0, 0);
  };

  return (
    <div className="font-sans text-stone-800 bg-stone-50 min-h-screen selection:bg-rose-200 selection:text-rose-900 relative">
      
      {/* 全域通知 (Toast) */}
      {notification && (
        <Toast 
          message={notification.message} 
          type={notification.type} 
          onClose={() => setNotification(null)} 
        />
      )}

      {/* Navbar */}
      {!(currentMode === 'creator' && !creatorUser) && (
        <Navbar 
          currentMode={currentMode} 
          setMode={handleModeSwitch} 
          cartItems={cartItems}
          isSearchOpen={isSearchOpen}
          onSearchClick={() => setIsSearchOpen(!isSearchOpen)}
          setSearchTerm={setSearchTerm}
          onCartClick={() => setIsCartOpen(!isCartOpen)}
          onMemberClick={() => {
              if(currentMode === 'customer') setCurrentView('member');
              else showNotification("創作者請直接登入後台", "error");
          }}
        />
      )}

      {/* Cart Sidebar */}
      {isCartOpen && (
        <>
          <div className="fixed inset-0 bg-black/20 z-40" onClick={() => setIsCartOpen(false)}></div>
          <div className="fixed top-0 right-0 h-full w-80 bg-white z-50 shadow-2xl animate-in slide-in-from-right duration-300 p-6 flex flex-col">
             <div className="flex justify-between items-center mb-6">
               <h2 className="font-serif font-bold text-xl">我的收藏 ({cartItems.length})</h2>
               <button onClick={() => setIsCartOpen(false)}><X size={24} className="text-stone-400 hover:text-stone-800"/></button>
             </div>
             <div className="flex-1 overflow-y-auto space-y-4">
               {cartItems.length === 0 ? (
                 <div className="text-center text-stone-400 mt-10">購物車還是空的<br/>去探索一些故事吧！</div>
               ) : (
                 cartItems.map((item, idx) => (
                   <div key={idx} className="flex gap-4 border-b pb-4">
                     <img src={item.image} className="w-16 h-16 object-cover rounded" alt={item.title}/>
                     <div className="flex-1">
                       <h4 className="font-bold text-sm text-stone-800">{item.title}</h4>
                       <p className="text-stone-500 text-sm">NT$ {item.price}</p>
                     </div>
                     <button onClick={() => handleRemoveFromCart(idx)} className="text-stone-300 hover:text-red-500"><Trash2 size={16}/></button>
                   </div>
                 ))
               )}
             </div>
             <div className="border-t pt-4 mt-4">
               <div className="flex justify-between items-center mb-4">
                 <span className="font-bold">總計</span>
                 <span className="font-bold text-xl">NT$ {cartTotal}</span>
               </div>
               <button onClick={() => {
                   if(cartItems.length === 0) showNotification("請先加入商品", "error");
                   else setIsCheckoutOpen(true);
               }} className="w-full bg-stone-900 text-white py-3 rounded font-bold hover:bg-stone-800 flex justify-center gap-2">
                 <CreditCard size={18}/> 前往結帳
               </button>
             </div>
          </div>
        </>
      )}

      <main>
        {/* 顧客端 */}
        {currentMode === 'customer' && (
          currentView === 'member' ? (
              <MemberProfile onBack={() => setCurrentView('home')} />
          ) : (
              <CustomerView 
                currentView={currentView} 
                setCurrentView={setCurrentView}
                selectedCreator={selectedCreator}
                setSelectedCreator={setSelectedCreator}
                selectedTheme={selectedTheme}
                setSelectedTheme={setSelectedTheme}
                addToCart={handleAddToCart}
                searchTerm={searchTerm}
                onNotify={showNotification}
              />
          )
        )}

        {/* 創作者端 */}
        {currentMode === 'creator' && (
           !creatorUser ? (
             <CreatorLogin 
               onLogin={() => setCreatorUser({ name: '秀琴姐' })} 
               onSwitchMode={setMode}
               onNotify={showNotification}
             />
           ) : (
             <CreatorDashboard 
                onLogout={() => { setCreatorUser(null); setMode('customer'); }} 
                onNotify={showNotification}
             />
           )
        )}

        {/* B2B 端 */}
        {currentMode === 'b2b' && <B2BPage onNotify={showNotification} />}
      </main>

      {/* Footer */}
      {!(currentMode === 'creator') && (
        <footer className="bg-stone-900 text-stone-400 py-12 px-4">
          <div className="max-w-7xl mx-auto grid md:grid-cols-4 gap-8">
            <div><h4 className="text-white font-serif text-xl mb-4">HerStory</h4><p className="text-sm">連結婦女創作者與世界的溫柔力量。</p></div>
            <div><h5 className="text-white font-bold mb-4">探索</h5><ul className="space-y-2 text-sm cursor-pointer"><li onClick={()=>document.getElementById('curation-wall')?.scrollIntoView({behavior:'smooth'})}>本週策展</li><li onClick={()=>{setCurrentView('home'); setSearchTerm(''); window.scrollTo(0,0);}}>創作者牆</li></ul></div>
            <div><h5 className="text-white font-bold mb-4">創作者服務</h5><ul className="space-y-2 text-sm cursor-pointer"><li onClick={()=>setMode('creator')}>創作者登入</li><li onClick={()=>setIsJoinModalOpen(true)}>加入我們</li></ul></div>
            <div><h5 className="text-white font-bold mb-4">企業合作</h5><button onClick={() => setMode('b2b')} className="text-emerald-400 text-sm hover:underline flex items-center gap-1"><Briefcase size={14} /> 前往 B2B 專區</button></div>
          </div>
          <div className="max-w-7xl mx-auto mt-12 pt-8 border-t border-stone-800 text-center text-xs">© 2024 HerStory Platform.</div>
        </footer>
      )}

      {/* 全域模態視窗 */}
      <CheckoutModal 
          isOpen={isCheckoutOpen} 
          onClose={() => setIsCheckoutOpen(false)} 
          total={cartTotal}
          onConfirm={() => {
              setCartItems([]);
              setIsCartOpen(false);
          }}
      />

      <JoinCreatorModal
          isOpen={isJoinModalOpen}
          onClose={() => setIsJoinModalOpen(false)}
          onNotify={showNotification}
      />
    </div>
  );
};

export default App;
