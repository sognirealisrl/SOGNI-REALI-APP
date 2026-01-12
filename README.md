# SOGNI-REALI-APP
import React, { useState, useEffect, useRef } from 'react';
import { Menu, X, ChevronRight, Sparkles, Zap, Shield, Star, ArrowRight, Circle } from 'lucide-react';
import { motion, useScroll, useTransform, useInView } from 'motion/react';

export default function App() {
  const [mobileMenuOpen, setMobileMenuOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);
  const { scrollYProgress } = useScroll();

  useEffect(() => {
    const handleScroll = () => {
      setScrolled(window.scrollY > 20);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  return (
    <div className="min-h-screen bg-black text-white overflow-hidden">
      {/* Animated Progress Bar */}
      <motion.div
        className="fixed top-0 left-0 right-0 h-1 bg-gradient-to-r from-blue-500 via-purple-500 to-pink-500 origin-left z-50"
        style={{ scaleX: scrollYProgress }}
      />

      {/* Navigation */}
      <nav className={`fixed w-full top-0 z-40 transition-all duration-500 ${
        scrolled ? 'bg-black/40 backdrop-blur-2xl border-b border-white/10' : 'bg-transparent'
      }`}>
        <div className="max-w-7xl mx-auto px-6 lg:px-8">
          <div className="flex items-center justify-between h-20">
            {/* Logo with Gradient */}
            <motion.div 
              className="flex-shrink-0"
              initial={{ opacity: 0, x: -20 }}
              animate={{ opacity: 1, x: 0 }}
              transition={{ duration: 0.6 }}
            >
              <h1 className="text-3xl tracking-tighter bg-gradient-to-r from-blue-400 via-purple-400 to-pink-400 bg-clip-text text-transparent">
                Sogni Reali
              </h1>
            </motion.div>

            {/* Desktop Navigation */}
            <div className="hidden md:flex items-center space-x-8">
              {['Prodotti', 'Innovazione', 'Visione', 'Contatti'].map((item, i) => (
                <motion.a
                  key={item}
                  href={`#${item.toLowerCase()}`}
                  className="text-sm text-white/70 hover:text-white transition-colors relative group"
                  initial={{ opacity: 0, y: -10 }}
                  animate={{ opacity: 1, y: 0 }}
                  transition={{ duration: 0.6, delay: i * 0.1 }}
                >
                  {item}
                  <span className="absolute -bottom-1 left-0 w-0 h-0.5 bg-gradient-to-r from-blue-400 to-purple-400 group-hover:w-full transition-all duration-300" />
                </motion.a>
              ))}
              <motion.button 
                className="bg-gradient-to-r from-blue-500 to-purple-600 text-white px-6 py-2.5 rounded-full text-sm hover:shadow-lg hover:shadow-purple-500/50 transition-all"
                initial={{ opacity: 0, scale: 0.8 }}
                animate={{ opacity: 1, scale: 1 }}
                transition={{ duration: 0.6, delay: 0.4 }}
                whileHover={{ scale: 1.05 }}
                whileTap={{ scale: 0.95 }}
              >
                Esplora
              </motion.button>
            </div>

            {/* Mobile menu button */}
            <button
              onClick={() => setMobileMenuOpen(!mobileMenuOpen)}
              className="md:hidden p-2 text-white"
            >
              {mobileMenuOpen ? <X size={24} /> : <Menu size={24} />}
            </button>
          </div>

          {/* Mobile Navigation */}
          {mobileMenuOpen && (
            <motion.div 
              className="md:hidden py-6 border-t border-white/10"
              initial={{ opacity: 0, height: 0 }}
              animate={{ opacity: 1, height: 'auto' }}
              exit={{ opacity: 0, height: 0 }}
            >
              <div className="flex flex-col space-y-4">
                {['Prodotti', 'Innovazione', 'Visione', 'Contatti'].map((item) => (
                  <a key={item} href={`#${item.toLowerCase()}`} className="text-sm text-white/70 hover:text-white">
                    {item}
                  </a>
                ))}
                <button className="bg-gradient-to-r from-blue-500 to-purple-600 text-white px-6 py-2.5 rounded-full text-sm w-full">
                  Esplora
                </button>
              </div>
            </motion.div>
          )}
        </div>
      </nav>

      {/* Hero Section - Futuristic */}
      <HeroSection />

      {/* Bento Grid Vision Section */}
      <BentoGridSection />

      {/* Products Section - Futuristic Cards */}
      <ProductsSection />

      {/* Features with Glassmorphism */}
      <FeaturesSection />

      {/* Interactive Stats Section */}
      <StatsSection />

      {/* Testimonials Carousel */}
      <TestimonialsSection />

      {/* CTA Section */}
      <CTASection />

      {/* Footer */}
      <FooterSection />
    </div>
  );
}

// Hero Section Component
function HeroSection() {
  const containerRef = useRef(null);
  const isInView = useInView(containerRef, { once: false, amount: 0.3 });

  return (
    <section ref={containerRef} className="relative min-h-screen flex items-center justify-center overflow-hidden pt-20">
      {/* Animated Background Gradient */}
      <div className="absolute inset-0 bg-gradient-to-br from-blue-950 via-purple-950 to-black">
        <div className="absolute inset-0 bg-[url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZGVmcz48cGF0dGVybiBpZD0iZ3JpZCIgd2lkdGg9IjQwIiBoZWlnaHQ9IjQwIiBwYXR0ZXJuVW5pdHM9InVzZXJTcGFjZU9uVXNlIj48cGF0aCBkPSJNIDQwIDAgTCAwIDAgMCA0MCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJyZ2JhKDI1NSwgMjU1LCAyNTUsIDAuMDUpIiBzdHJva2Utd2lkdGg9IjEiLz48L3BhdHRlcm4+PC9kZWZzPjxyZWN0IHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIGZpbGw9InVybCgjZ3JpZCkiLz48L3N2Zz4=')] opacity-40" />
      </div>

      {/* Floating Orbs */}
      <motion.div
        className="absolute top-1/4 left-1/4 w-96 h-96 bg-blue-500/30 rounded-full blur-3xl"
        animate={{
          scale: [1, 1.2, 1],
          opacity: [0.3, 0.5, 0.3],
        }}
        transition={{ duration: 8, repeat: Infinity, ease: "easeInOut" }}
      />
      <motion.div
        className="absolute bottom-1/4 right-1/4 w-96 h-96 bg-purple-500/30 rounded-full blur-3xl"
        animate={{
          scale: [1.2, 1, 1.2],
          opacity: [0.5, 0.3, 0.5],
        }}
        transition={{ duration: 8, repeat: Infinity, ease: "easeInOut" }}
      />

      {/* Content */}
      <div className="relative z-10 text-center px-6 max-w-6xl mx-auto">
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 30 }}
          transition={{ duration: 1 }}
        >
          <motion.div
            className="inline-block mb-6 px-4 py-2 bg-white/10 backdrop-blur-xl border border-white/20 rounded-full text-sm"
            initial={{ opacity: 0, scale: 0.8 }}
            animate={isInView ? { opacity: 1, scale: 1 } : { opacity: 0, scale: 0.8 }}
            transition={{ duration: 0.6 }}
          >
            <span className="bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">
              ✨ Benvenuti nel Futuro
            </span>
          </motion.div>

          <h1 className="text-6xl md:text-8xl lg:text-9xl mb-8 tracking-tighter">
            <span className="bg-gradient-to-r from-white via-blue-100 to-purple-100 bg-clip-text text-transparent">
              Sogni Reali
            </span>
          </h1>

          <p className="text-xl md:text-3xl text-white/70 mb-12 max-w-4xl mx-auto leading-relaxed">
            Dove l'<span className="text-white">innovazione incontra l'eleganza</span>,
            <br />trasformando visioni in <span className="bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">realtà straordinarie</span>
          </p>

          <div className="flex flex-col sm:flex-row gap-4 justify-center items-center">
            <motion.button
              className="group bg-white text-black px-8 py-4 rounded-full hover:shadow-2xl hover:shadow-white/20 transition-all flex items-center gap-2"
              whileHover={{ scale: 1.05 }}
              whileTap={{ scale: 0.95 }}
            >
              Inizia il Viaggio
              <ArrowRight className="group-hover:translate-x-1 transition-transform" size={20} />
            </motion.button>
            <motion.button
              className="group border-2 border-white/30 text-white px-8 py-4 rounded-full hover:bg-white/10 backdrop-blur-xl transition-all flex items-center gap-2"
              whileHover={{ scale: 1.05 }}
              whileTap={{ scale: 0.95 }}
            >
              <Circle className="w-4 h-4 fill-white" />
              Guarda il Video
            </motion.button>
          </div>
        </motion.div>

        {/* Scroll Indicator */}
        <motion.div
          className="absolute bottom-8 left-1/2 -translate-x-1/2"
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          transition={{ delay: 1.5 }}
        >
          <motion.div
            className="w-6 h-10 border-2 border-white/30 rounded-full flex justify-center pt-2"
            animate={{ y: [0, 10, 0] }}
            transition={{ duration: 2, repeat: Infinity }}
          >
            <div className="w-1 h-2 bg-white/50 rounded-full" />
          </motion.div>
        </motion.div>
      </div>
    </section>
  );
}

// Bento Grid Section
function BentoGridSection() {
  const containerRef = useRef(null);
  const isInView = useInView(containerRef, { once: false, amount: 0.2 });

  return (
    <section ref={containerRef} className="py-32 px-6 relative overflow-hidden">
      <div className="max-w-7xl mx-auto">
        <motion.div
          className="text-center mb-20"
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 30 }}
          transition={{ duration: 0.8 }}
        >
          <h2 className="text-5xl md:text-7xl mb-6 tracking-tighter bg-gradient-to-r from-white to-white/60 bg-clip-text text-transparent">
            La Nostra Visione
          </h2>
          <p className="text-xl text-white/60 max-w-2xl mx-auto">
            Progettare il domani, oggi
          </p>
        </motion.div>

        <div className="grid grid-cols-1 md:grid-cols-3 gap-6 auto-rows-[280px]">
          {/* Large Card */}
          <motion.div
            className="md:col-span-2 md:row-span-2 relative group overflow-hidden rounded-3xl bg-gradient-to-br from-blue-900/40 to-purple-900/40 backdrop-blur-xl border border-white/10 p-8"
            initial={{ opacity: 0, scale: 0.9 }}
            animate={isInView ? { opacity: 1, scale: 1 } : { opacity: 0, scale: 0.9 }}
            transition={{ duration: 0.6, delay: 0.1 }}
            whileHover={{ scale: 1.02 }}
          >
            <div className="absolute inset-0 bg-gradient-to-br from-blue-500/20 to-purple-500/20 opacity-0 group-hover:opacity-100 transition-opacity duration-500" />
            <div className="relative z-10 h-full flex flex-col justify-between">
              <div>
                <Sparkles className="w-12 h-12 mb-4 text-blue-400" />
                <h3 className="text-4xl mb-4 tracking-tight">Innovazione Continua</h3>
                <p className="text-white/70 text-lg leading-relaxed">
                  Spingiamo costantemente i confini della tecnologia e del design per creare esperienze
                  che ridefiniscono il possibile.
                </p>
              </div>
              <div className="flex items-center gap-2 text-blue-400 group-hover:gap-3 transition-all">
                Esplora <ArrowRight size={20} />
              </div>
            </div>
          </motion.div>

          {/* Small Cards */}
          <motion.div
            className="relative group overflow-hidden rounded-3xl bg-gradient-to-br from-purple-900/40 to-pink-900/40 backdrop-blur-xl border border-white/10 p-8"
            initial={{ opacity: 0, scale: 0.9 }}
            animate={isInView ? { opacity: 1, scale: 1 } : { opacity: 0, scale: 0.9 }}
            transition={{ duration: 0.6, delay: 0.2 }}
            whileHover={{ scale: 1.05 }}
          >
            <Zap className="w-10 h-10 mb-4 text-purple-400" />
            <h3 className="text-2xl mb-2 tracking-tight">Velocità</h3>
            <p className="text-white/60 text-sm">Performance fulminee</p>
          </motion.div>

          <motion.div
            className="relative group overflow-hidden rounded-3xl bg-gradient-to-br from-pink-900/40 to-orange-900/40 backdrop-blur-xl border border-white/10 p-8"
            initial={{ opacity: 0, scale: 0.9 }}
            animate={isInView ? { opacity: 1, scale: 1 } : { opacity: 0, scale: 0.9 }}
            transition={{ duration: 0.6, delay: 0.3 }}
            whileHover={{ scale: 1.05 }}
          >
            <Shield className="w-10 h-10 mb-4 text-pink-400" />
            <h3 className="text-2xl mb-2 tracking-tight">Sicurezza</h3>
            <p className="text-white/60 text-sm">Protezione totale</p>
          </motion.div>

          <motion.div
            className="md:col-span-2 relative group overflow-hidden rounded-3xl bg-gradient-to-br from-cyan-900/40 to-blue-900/40 backdrop-blur-xl border border-white/10 p-8"
            initial={{ opacity: 0, scale: 0.9 }}
            animate={isInView ? { opacity: 1, scale: 1 } : { opacity: 0, scale: 0.9 }}
            transition={{ duration: 0.6, delay: 0.4 }}
            whileHover={{ scale: 1.02 }}
          >
            <div className="h-full flex flex-col justify-between">
              <div>
                <h3 className="text-3xl mb-4 tracking-tight">Design del Futuro</h3>
                <p className="text-white/70 leading-relaxed">
                  Interfacce che anticipano le tue necessità con intelligenza artificiale integrata
                </p>
              </div>
              <div className="flex gap-2">
                {[...Array(3)].map((_, i) => (
                  <div key={i} className="w-2 h-2 rounded-full bg-gradient-to-r from-cyan-400 to-blue-400" />
                ))}
              </div>
            </div>
          </motion.div>
        </div>
      </div>
    </section>
  );
}

// Products Section
function ProductsSection() {
  const containerRef = useRef(null);
  const isInView = useInView(containerRef, { once: false, amount: 0.2 });

  const products = [
    {
      title: 'Quantum Series',
      description: 'La prossima generazione di tecnologia intelligente',
      price: '€2,999',
      badge: 'Nuovo',
      gradient: 'from-blue-500 to-cyan-500',
    },
    {
      title: 'Nebula Collection',
      description: 'Design che sfida la gravità e il tempo',
      price: '€1,999',
      badge: 'Bestseller',
      gradient: 'from-purple-500 to-pink-500',
    },
    {
      title: 'Infinity Edition',
      description: 'Dove l\'eleganza incontra l\'eternità',
      price: '€3,999',
      badge: 'Limitata',
      gradient: 'from-orange-500 to-red-500',
    },
  ];

  return (
    <section id="prodotti" ref={containerRef} className="py-32 px-6 relative">
      <div className="max-w-7xl mx-auto">
        <motion.div
          className="text-center mb-20"
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 30 }}
          transition={{ duration: 0.8 }}
        >
          <h2 className="text-5xl md:text-7xl mb-6 tracking-tighter bg-gradient-to-r from-white to-white/60 bg-clip-text text-transparent">
            Collezione 2026
          </h2>
          <p className="text-xl text-white/60 max-w-2xl mx-auto">
            Esperienza il futuro attraverso il design
          </p>
        </motion.div>

        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {products.map((product, index) => (
            <motion.div
              key={index}
              className="group relative overflow-hidden rounded-3xl bg-white/5 backdrop-blur-xl border border-white/10 hover:border-white/30 transition-all duration-500"
              initial={{ opacity: 0, y: 50 }}
              animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 50 }}
              transition={{ duration: 0.6, delay: index * 0.1 }}
              whileHover={{ y: -10 }}
            >
              {/* Badge */}
              {product.badge && (
                <div className={`absolute top-6 right-6 bg-gradient-to-r ${product.gradient} text-white px-4 py-2 rounded-full text-xs z-10 font-semibold`}>
                  {product.badge}
                </div>
              )}

              {/* Image Placeholder with Gradient */}
              <div className={`relative h-80 bg-gradient-to-br ${product.gradient} opacity-60`}>
                <div className="absolute inset-0 bg-black/20" />
                <motion.div
                  className="absolute inset-0 bg-white/10"
                  initial={{ scale: 1 }}
                  whileHover={{ scale: 1.1 }}
                  transition={{ duration: 0.6 }}
                />
              </div>

              {/* Content */}
              <div className="p-8">
                <h3 className="text-3xl mb-3 tracking-tight">{product.title}</h3>
                <p className="text-white/60 mb-6 leading-relaxed">{product.description}</p>

                <div className="flex items-center justify-between">
                  <div className="text-2xl font-light">{product.price}</div>
                  <motion.button
                    className="flex items-center gap-2 text-sm bg-white/10 px-4 py-2 rounded-full group-hover:bg-white/20 transition-all"
                    whileHover={{ gap: '12px' }}
                  >
                    Scopri
                    <ArrowRight size={16} />
                  </motion.button>
                </div>
              </div>
            </motion.div>
          ))}
        </div>
      </div>
    </section>
  );
}

// Features Section
function FeaturesSection() {
  const containerRef = useRef(null);
  const isInView = useInView(containerRef, { once: false, amount: 0.2 });

  const features = [
    {
      icon: <Sparkles className="w-8 h-8" />,
      title: 'AI Integrata',
      description: 'Intelligenza artificiale avanzata che apprende dalle tue preferenze',
      color: 'blue',
    },
    {
      icon: <Zap className="w-8 h-8" />,
      title: 'Ultra Performance',
      description: 'Processori quantistici per velocità senza precedenti',
      color: 'purple',
    },
    {
      icon: <Shield className="w-8 h-8" />,
      title: 'Sicurezza Biometrica',
      description: 'Protezione avanzata con riconoscimento multi-livello',
      color: 'pink',
    },
  ];

  return (
    <section id="innovazione" ref={containerRef} className="py-32 px-6 relative overflow-hidden">
      {/* Background Glow */}
      <div className="absolute inset-0 bg-gradient-to-b from-transparent via-blue-950/20 to-transparent" />

      <div className="max-w-7xl mx-auto relative z-10">
        <motion.div
          className="text-center mb-20"
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 30 }}
          transition={{ duration: 0.8 }}
        >
          <h2 className="text-5xl md:text-7xl mb-6 tracking-tighter bg-gradient-to-r from-white to-white/60 bg-clip-text text-transparent">
            Tecnologia Avanzata
          </h2>
          <p className="text-xl text-white/60 max-w-2xl mx-auto">
            Innovazioni che ridefiniscono il possibile
          </p>
        </motion.div>

        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {features.map((feature, index) => (
            <motion.div
              key={index}
              className={`group relative p-8 rounded-3xl bg-gradient-to-br from-white/5 to-white/[0.02] backdrop-blur-xl border border-white/10 hover:border-${feature.color}-500/50 transition-all duration-500`}
              initial={{ opacity: 0, y: 50 }}
              animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 50 }}
              transition={{ duration: 0.6, delay: index * 0.15 }}
              whileHover={{ y: -10 }}
            >
              {/* Icon Container */}
              <motion.div
                className={`inline-flex items-center justify-center w-16 h-16 rounded-2xl bg-gradient-to-br from-${feature.color}-500/20 to-${feature.color}-600/20 mb-6 group-hover:scale-110 transition-transform duration-300`}
                whileHover={{ rotate: 360 }}
                transition={{ duration: 0.6 }}
              >
                <div className={`text-${feature.color}-400`}>
                  {feature.icon}
                </div>
              </motion.div>

              <h3 className="text-2xl mb-4 tracking-tight">{feature.title}</h3>
              <p className="text-white/60 leading-relaxed">{feature.description}</p>

              {/* Hover Glow Effect */}
              <div className={`absolute inset-0 rounded-3xl bg-gradient-to-br from-${feature.color}-500/0 to-${feature.color}-600/0 group-hover:from-${feature.color}-500/10 group-hover:to-${feature.color}-600/10 transition-all duration-500 -z-10`} />
            </motion.div>
          ))}
        </div>
      </div>
    </section>
  );
}

// Stats Section
function StatsSection() {
  const containerRef = useRef(null);
  const isInView = useInView(containerRef, { once: false, amount: 0.3 });

  const stats = [
    { value: '50K+', label: 'Clienti Soddisfatti' },
    { value: '200+', label: 'Premi Vinti' },
    { value: '99.9%', label: 'Affidabilità' },
    { value: '24/7', label: 'Supporto' },
  ];

  return (
    <section ref={containerRef} className="py-32 px-6 relative">
      <div className="max-w-7xl mx-auto">
        <div className="grid grid-cols-2 md:grid-cols-4 gap-8">
          {stats.map((stat, index) => (
            <motion.div
              key={index}
              className="text-center"
              initial={{ opacity: 0, scale: 0.5 }}
              animate={isInView ? { opacity: 1, scale: 1 } : { opacity: 0, scale: 0.5 }}
              transition={{ duration: 0.5, delay: index * 0.1 }}
            >
              <motion.div
                className="text-5xl md:text-6xl mb-3 bg-gradient-to-r from-blue-400 via-purple-400 to-pink-400 bg-clip-text text-transparent"
                initial={{ opacity: 0 }}
                animate={isInView ? { opacity: 1 } : { opacity: 0 }}
                transition={{ duration: 1, delay: index * 0.1 }}
              >
                {stat.value}
              </motion.div>
              <div className="text-white/60">{stat.label}</div>
            </motion.div>
          ))}
        </div>
      </div>
    </section>
  );
}

// Testimonials Section
function TestimonialsSection() {
  const containerRef = useRef(null);
  const isInView = useInView(containerRef, { once: false, amount: 0.2 });

  const testimonials = [
    {
      text: "Sogni Reali ha letteralmente trasformato la mia vita quotidiana. La tecnologia è anni luce avanti.",
      author: "Marco Rossi",
      role: "CEO, TechVision",
      rating: 5,
    },
    {
      text: "Design impeccabile e prestazioni straordinarie. Non potrei chiedere di meglio.",
      author: "Sofia Bianchi",
      role: "Designer Innovazione",
      rating: 5,
    },
    {
      text: "Il futuro è qui, e si chiama Sogni Reali. Semplicemente incredibile.",
      author: "Alessandro Conti",
      role: "Architetto",
      rating: 5,
    },
  ];

  return (
    <section ref={containerRef} className="py-32 px-6 relative overflow-hidden">
      {/* Background Gradient */}
      <div className="absolute inset-0 bg-gradient-to-b from-purple-950/20 via-transparent to-blue-950/20" />

      <div className="max-w-7xl mx-auto relative z-10">
        <motion.div
          className="text-center mb-20"
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 30 }}
          transition={{ duration: 0.8 }}
        >
          <h2 className="text-5xl md:text-7xl mb-6 tracking-tighter bg-gradient-to-r from-white to-white/60 bg-clip-text text-transparent">
            Storie di Successo
          </h2>
          <p className="text-xl text-white/60 max-w-2xl mx-auto">
            Cosa dicono i nostri visionari
          </p>
        </motion.div>

        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {testimonials.map((testimonial, index) => (
            <motion.div
              key={index}
              className="relative p-8 rounded-3xl bg-gradient-to-br from-white/10 to-white/[0.02] backdrop-blur-2xl border border-white/20"
              initial={{ opacity: 0, y: 50 }}
              animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 50 }}
              transition={{ duration: 0.6, delay: index * 0.15 }}
              whileHover={{ scale: 1.05, borderColor: 'rgba(255, 255, 255, 0.4)' }}
            >
              {/* Stars */}
              <div className="flex gap-1 mb-6">
                {[...Array(testimonial.rating)].map((_, i) => (
                  <Star key={i} size={18} className="fill-yellow-400 text-yellow-400" />
                ))}
              </div>

              {/* Quote */}
              <p className="text-lg mb-8 leading-relaxed text-white/80">
                "{testimonial.text}"
              </p>

              {/* Author */}
              <div className="flex items-center gap-4">
                <div className="w-12 h-12 rounded-full bg-gradient-to-br from-blue-400 to-purple-600" />
                <div>
                  <div className="font-semibold text-white">{testimonial.author}</div>
                  <div className="text-sm text-white/60">{testimonial.role}</div>
                </div>
              </div>

              {/* Glow Effect */}
              <div className="absolute -inset-px rounded-3xl bg-gradient-to-br from-blue-500/20 to-purple-500/20 opacity-0 group-hover:opacity-100 transition-opacity duration-500 -z-10 blur-xl" />
            </motion.div>
          ))}
        </div>
      </div>
    </section>
  );
}

// CTA Section
function CTASection() {
  const containerRef = useRef(null);
  const isInView = useInView(containerRef, { once: false, amount: 0.3 });

  return (
    <section id="visione" ref={containerRef} className="py-32 px-6 relative overflow-hidden">
      {/* Animated Background */}
      <div className="absolute inset-0">
        <div className="absolute inset-0 bg-gradient-to-r from-blue-600/20 via-purple-600/20 to-pink-600/20" />
        <motion.div
          className="absolute inset-0 bg-gradient-to-r from-blue-500/30 via-purple-500/30 to-pink-500/30"
          animate={{
            backgroundPosition: ['0% 50%', '100% 50%', '0% 50%'],
          }}
          transition={{ duration: 10, repeat: Infinity, ease: 'linear' }}
          style={{ backgroundSize: '200% 200%' }}
        />
      </div>

      <div className="max-w-4xl mx-auto text-center relative z-10">
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          animate={isInView ? { opacity: 1, y: 0 } : { opacity: 0, y: 30 }}
          transition={{ duration: 0.8 }}
        >
          <h2 className="text-5xl md:text-7xl mb-8 tracking-tighter">
            Pronto per il Futuro?
          </h2>
          <p className="text-xl md:text-2xl text-white/70 mb-12 max-w-2xl mx-auto leading-relaxed">
            Unisciti a migliaia di visionari che hanno già scelto l'eccellenza
          </p>

          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <motion.button
              className="group bg-white text-black px-10 py-5 rounded-full text-lg hover:shadow-2xl hover:shadow-white/30 transition-all flex items-center justify-center gap-2"
              whileHover={{ scale: 1.05 }}
              whileTap={{ scale: 0.95 }}
            >
              Esplora la Collezione
              <ArrowRight className="group-hover:translate-x-1 transition-transform" size={20} />
            </motion.button>
            <motion.button
              className="border-2 border-white/30 text-white px-10 py-5 rounded-full text-lg hover:bg-white/10 backdrop-blur-xl transition-all"
              whileHover={{ scale: 1.05 }}
              whileTap={{ scale: 0.95 }}
            >
              Richiedi Demo
            </motion.button>
          </div>
        </motion.div>
      </div>
    </section>
  );
}

// Footer Section
function FooterSection() {
  return (
    <footer id="contatti" className="relative py-20 px-6 border-t border-white/10">
      <div className="max-w-7xl mx-auto">
        <div className="grid grid-cols-1 md:grid-cols-4 gap-12 mb-16">
          {/* Brand */}
          <div className="md:col-span-2">
            <h3 className="text-3xl mb-6 tracking-tighter bg-gradient-to-r from-blue-400 via-purple-400 to-pink-400 bg-clip-text text-transparent">
              Sogni Reali
            </h3>
            <p className="text-white/60 leading-relaxed mb-6 max-w-md">
              Trasformiamo visioni audaci in realtà straordinarie attraverso design rivoluzionario
              e tecnologia all'avanguardia.
            </p>
            <div className="flex gap-4">
              {['Twitter', 'Instagram', 'LinkedIn'].map((social) => (
                <motion.a
                  key={social}
                  href="#"
                  className="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center hover:bg-white/10 hover:border-white/20 transition-all"
                  whileHover={{ scale: 1.1 }}
                  whileTap={{ scale: 0.9 }}
                >
                  <span className="text-xs">{social[0]}</span>
                </motion.a>
              ))}
            </div>
          </div>

          {/* Links */}
          <div>
            <h4 className="text-lg mb-6 font-semibold">Esplora</h4>
            <ul className="space-y-3">
              {['Prodotti', 'Innovazione', 'Visione', 'Carriere'].map((link) => (
                <li key={link}>
                  <a href="#" className="text-white/60 hover:text-white transition-colors">
                    {link}
                  </a>
                </li>
              ))}
            </ul>
          </div>

          <div>
            <h4 className="text-lg mb-6 font-semibold">Supporto</h4>
            <ul className="space-y-3">
              {['Contatti', 'FAQ', 'Documentazione', 'Assistenza'].map((link) => (
                <li key={link}>
                  <a href="#" className="text-white/60 hover:text-white transition-colors">
                    {link}
                  </a>
                </li>
              ))}
            </ul>
          </div>
        </div>

        {/* Bottom Bar */}
        <div className="pt-8 border-t border-white/10 flex flex-col md:flex-row justify-between items-center gap-4">
          <p className="text-white/40 text-sm">
            © 2026 Sogni Reali. Tutti i diritti riservati.
          </p>
          <div className="flex gap-6 text-sm text-white/40">
            {['Privacy', 'Termini', 'Cookie'].map((link) => (
              <a key={link} href="#" className="hover:text-white/60 transition-colors">
                {link}
              </a>
            ))}
          </div>
        </div>
      </div>
    </footer>
  );
}
