import { useEffect, useRef } from "react";
import * as THREE from "three";
import { motion } from "motion/react";
import React from "react";

function RubiksCube() {
  const mountRef = useRef<HTMLDivElement>(null);
  const sceneRef = useRef<{
    renderer: THREE.WebGLRenderer;
    animFrameId: number;
  } | null>(null);
  const isDragging = useRef(false);
  const previousMouse = useRef({ x: 0, y: 0 });
  const rotVelocity = useRef({ x: 0, y: 0 });
  const cubeGroupRef = useRef<THREE.Group | null>(null);
  const cubiesRef = useRef<{ mesh: THREE.Mesh; wire: THREE.LineSegments; origPos: THREE.Vector3 }[]>([]);
  const explodeStateRef = useRef<"idle" | "exploding" | "collecting">("idle");
  const explodeTargetsRef = useRef<THREE.Vector3[]>([]);
  const explodeProgressRef = useRef(0);

  useEffect(() => {
    if (!mountRef.current) return;

    const width = mountRef.current.clientWidth;
    const height = mountRef.current.clientHeight;

    const scene = new THREE.Scene();
    scene.background = null;

    const camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 100);
    camera.position.set(4, 4, 6);
    camera.lookAt(0, 0, 0);

    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    renderer.setSize(width, height);
    renderer.setPixelRatio(window.devicePixelRatio);
    mountRef.current.appendChild(renderer.domElement);

    const ambient = new THREE.AmbientLight(0xffffff, 0.05);
    scene.add(ambient);

    const frontRight = new THREE.DirectionalLight(0xffffff, 6);
    frontRight.position.set(6, 5, 10);
    scene.add(frontRight);

    const topLight = new THREE.DirectionalLight(0xffffff, 2.5);
    topLight.position.set(2, 12, 4);
    scene.add(topLight);

    const rimLight = new THREE.DirectionalLight(0xaaccff, 1.5);
    rimLight.position.set(-8, 3, -5);
    scene.add(rimLight);

    const movingLight = new THREE.PointLight(0xffffff, 2, 20);
    movingLight.position.set(4, 4, 6);
    scene.add(movingLight);

    const cubeGroup = new THREE.Group();
    cubeGroupRef.current = cubeGroup;
    const size = 1;
    const gap = 0.06;
    const cubies: { mesh: THREE.Mesh; wire: THREE.LineSegments; origPos: THREE.Vector3 }[] = [];

    for (let x = -1; x <= 1; x++) {
      for (let y = -1; y <= 1; y++) {
        for (let z = -1; z <= 1; z++) {
          const geo = new THREE.BoxGeometry(size, size, size);
          const mat = new THREE.MeshPhysicalMaterial({
            color: "#050505",
            roughness: 0.0,
            metalness: 0.1,
            reflectivity: 1,
            clearcoat: 1,
            clearcoatRoughness: 0.0,
            envMapIntensity: 2,
          });
          const cubie = new THREE.Mesh(geo, mat);
          const pos = new THREE.Vector3(x * (size + gap), y * (size + gap), z * (size + gap));
          cubie.position.copy(pos);
          cubeGroup.add(cubie);

          const edges = new THREE.EdgesGeometry(geo);
          const lineMat = new THREE.LineBasicMaterial({ color: "#ffffff", transparent: true, opacity: 0.35 });
          const wireframe = new THREE.LineSegments(edges, lineMat);
          wireframe.position.copy(pos);
          cubeGroup.add(wireframe);

          cubies.push({ mesh: cubie, wire: wireframe, origPos: pos.clone() });
        }
      }
    }

    cubiesRef.current = cubies;
    scene.add(cubeGroup);
    cubeGroup.rotation.x = 0.38;
    cubeGroup.rotation.y = 0.55;

    const generateScatterTargets = () => {
      return cubies.map((c) => new THREE.Vector3(
        c.origPos.x + (Math.random() - 0.5) * 1.6,
        c.origPos.y + (Math.random() - 0.5) * 1.6,
        c.origPos.z + (Math.random() - 0.5) * 1.6,
      ));
    };

    const explodeInterval = setInterval(() => {
      if (explodeStateRef.current === "idle") {
        explodeTargetsRef.current = generateScatterTargets();
        explodeStateRef.current = "exploding";
        explodeProgressRef.current = 0;
      }
    }, 10000);

    let animFrameId = 0;
    let t = 0;

    const easeInOut = (v: number) => v < 0.5 ? 2 * v * v : -1 + (4 - 2 * v) * v;

    const animate = () => {
      animFrameId = requestAnimationFrame(animate);
      t += 0.012;

      movingLight.position.x = Math.sin(t * 0.8) * 6;
      movingLight.position.y = Math.cos(t * 0.5) * 4;
      movingLight.position.z = Math.abs(Math.sin(t * 0.4)) * 5 + 6;

      if (explodeStateRef.current === "exploding") {
        explodeProgressRef.current += 0.018;
        const p = Math.min(explodeProgressRef.current, 1);
        const ep = easeInOut(p);
        cubies.forEach((c, i) => {
          c.mesh.position.lerpVectors(c.origPos, explodeTargetsRef.current[i], ep);
          c.wire.position.copy(c.mesh.position);
        });
        if (p >= 1) {
          explodeStateRef.current = "collecting";
          explodeProgressRef.current = 0;
        }
      } else if (explodeStateRef.current === "collecting") {
        explodeProgressRef.current += 0.022;
        const p = Math.min(explodeProgressRef.current, 1);
        const ep = easeInOut(p);
        cubies.forEach((c, i) => {
          c.mesh.position.lerpVectors(explodeTargetsRef.current[i], c.origPos, ep);
          c.wire.position.copy(c.mesh.position);
        });
        if (p >= 1) {
          explodeStateRef.current = "idle";
          cubies.forEach(c => {
            c.mesh.position.copy(c.origPos);
            c.wire.position.copy(c.origPos);
          });
        }
      }

      if (!isDragging.current) {
        cubeGroup.rotation.y += 0.007;
        rotVelocity.current.x *= 0.93;
        rotVelocity.current.y *= 0.93;
        cubeGroup.rotation.x += rotVelocity.current.x * 0.008;
        cubeGroup.rotation.y += rotVelocity.current.y * 0.008;
      }

      renderer.render(scene, camera);
    };
    animate();

    sceneRef.current = { renderer, animFrameId };

    const el = mountRef.current;

    const onMouseDown = (e: MouseEvent) => {
      isDragging.current = true;
      previousMouse.current = { x: e.clientX, y: e.clientY };
      rotVelocity.current = { x: 0, y: 0 };
    };
    const onMouseMove = (e: MouseEvent) => {
      if (!isDragging.current || !cubeGroupRef.current) return;
      const dx = e.clientX - previousMouse.current.x;
      const dy = e.clientY - previousMouse.current.y;
      cubeGroupRef.current.rotation.y += dx * 0.011;
      cubeGroupRef.current.rotation.x += dy * 0.011;
      rotVelocity.current = { x: dy, y: dx };
      previousMouse.current = { x: e.clientX, y: e.clientY };
    };
    const onMouseUp = () => { isDragging.current = false; };

    const onTouchStart = (e: TouchEvent) => {
      isDragging.current = true;
      const touch = e.touches[0];
      previousMouse.current = { x: touch.clientX, y: touch.clientY };
      rotVelocity.current = { x: 0, y: 0 };
    };
    const onTouchMove = (e: TouchEvent) => {
      if (!isDragging.current || !cubeGroupRef.current) return;
      const touch = e.touches[0];
      const dx = touch.clientX - previousMouse.current.x;
      const dy = touch.clientY - previousMouse.current.y;
      cubeGroupRef.current.rotation.y += dx * 0.013;
      cubeGroupRef.current.rotation.x += dy * 0.013;
      rotVelocity.current = { x: dy, y: dx };
      previousMouse.current = { x: touch.clientX, y: touch.clientY };
    };
    const onTouchEnd = () => { isDragging.current = false; };

    el.addEventListener("mousedown", onMouseDown);
    window.addEventListener("mousemove", onMouseMove);
    window.addEventListener("mouseup", onMouseUp);
    el.addEventListener("touchstart", onTouchStart, { passive: true });
    window.addEventListener("touchmove", onTouchMove, { passive: true });
    window.addEventListener("touchend", onTouchEnd);

    const onResize = () => {
      if (!mountRef.current || !sceneRef.current) return;
      const w = mountRef.current.clientWidth;
      const h = mountRef.current.clientHeight;
      camera.aspect = w / h;
      camera.updateProjectionMatrix();
      renderer.setSize(w, h);
    };
    window.addEventListener("resize", onResize);

    return () => {
      clearInterval(explodeInterval);
      cancelAnimationFrame(animFrameId);
      el.removeEventListener("mousedown", onMouseDown);
      window.removeEventListener("mousemove", onMouseMove);
      window.removeEventListener("mouseup", onMouseUp);
      el.removeEventListener("touchstart", onTouchStart);
      window.removeEventListener("touchmove", onTouchMove);
      window.removeEventListener("touchend", onTouchEnd);
      window.removeEventListener("resize", onResize);
      renderer.dispose();
      if (mountRef.current && renderer.domElement.parentNode === mountRef.current) {
        mountRef.current.removeChild(renderer.domElement);
      }
    };
  }, []);

  return (
    <div
      ref={mountRef}
      className="w-[260px] h-[260px] md:w-[300px] md:h-[300px] cursor-grab active:cursor-grabbing"
      style={{
        filter: "drop-shadow(0 0 28px rgba(255,255,255,0.22)) drop-shadow(0 0 8px rgba(255,255,255,0.1))",
      }}
    />
  );
}

function StarField() {
  const canvasRef = useRef<HTMLCanvasElement>(null);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas) return;
    const ctx = canvas.getContext("2d");
    if (!ctx) return;

    const resize = () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    };
    resize();
    window.addEventListener("resize", resize);

    const STAR_COUNT = 350;
    const stars = Array.from({ length: STAR_COUNT }, () => ({
      x: Math.random() * window.innerWidth,
      y: Math.random() * window.innerHeight,
      size: Math.random() * 0.9 + 0.1,
      speed: Math.random() * 0.5 + 0.15,
      opacity: Math.random() * 0.8 + 0.15,
    }));

    let animId = 0;
    const draw = () => {
      animId = requestAnimationFrame(draw);
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      for (const star of stars) {
        star.x += star.speed * 0.55;
        star.y += star.speed;

        if (star.y > canvas.height + 2 || star.x > canvas.width + 2) {
          const fromTop = Math.random() > 0.5;
          if (fromTop) {
            star.x = Math.random() * canvas.width;
            star.y = -2;
          } else {
            star.x = -2;
            star.y = Math.random() * canvas.height;
          }
        }

        ctx.beginPath();
        ctx.arc(star.x, star.y, star.size, 0, Math.PI * 2);
        const grd = ctx.createRadialGradient(star.x, star.y, 0, star.x, star.y, star.size * 2.5);
        grd.addColorStop(0, `rgba(255,255,255,${star.opacity})`);
        grd.addColorStop(0.4, `rgba(220,240,255,${star.opacity * 0.6})`);
        grd.addColorStop(1, `rgba(255,255,255,0)`);
        ctx.fillStyle = grd;
        ctx.fill();
      }
    };
    draw();

    return () => {
      cancelAnimationFrame(animId);
      window.removeEventListener("resize", resize);
    };
  }, []);

  return (
    <canvas
      ref={canvasRef}
      className="fixed inset-0 pointer-events-none"
      style={{ zIndex: 0 }}
    />
  );
}

function IntroAnimation({ onDone }: { onDone: () => void }) {
  const mountRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    if (!mountRef.current) return;
    const w = window.innerWidth;
    const h = window.innerHeight;

    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(55, w / h, 0.1, 400);
    camera.position.set(5, 5, 16);
    camera.lookAt(0, 0, 0);

    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: false });
    renderer.setClearColor(0x000000, 1);
    renderer.setSize(w, h);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    mountRef.current.appendChild(renderer.domElement);

    scene.add(new THREE.AmbientLight(0xffffff, 0.05));
    const fl = new THREE.DirectionalLight(0xffffff, 6);
    fl.position.set(6, 5, 10); scene.add(fl);
    const tl = new THREE.DirectionalLight(0xffffff, 2.5);
    tl.position.set(2, 12, 4); scene.add(tl);
    const rl = new THREE.DirectionalLight(0xaaccff, 1.5);
    rl.position.set(-8, 3, -5); scene.add(rl);

    const SIZE = 1;
    const GAP = 0.06;
    const step = SIZE + GAP;

    type IntroCube = {
      group: THREE.Group;
      sx: number; sy: number; sz: number;
      tx: number; ty: number; tz: number;
      rx: number; ry: number; rz: number;
      delay: number;
      progress: number;
      speed: number;
    };

    const introCubes: IntroCube[] = [];
    let idx = 0;

    for (let x = -1; x <= 1; x++) {
      for (let y = -1; y <= 1; y++) {
        for (let z = -1; z <= 1; z++) {
          const geo = new THREE.BoxGeometry(SIZE, SIZE, SIZE);
          const mat = new THREE.MeshPhysicalMaterial({
            color: "#050505",
            roughness: 0.0,
            metalness: 0.1,
            clearcoat: 1,
            clearcoatRoughness: 0.0,
            reflectivity: 1,
          });
          const mesh = new THREE.Mesh(geo, mat);
          const edges = new THREE.EdgesGeometry(geo);
          const lineMat = new THREE.LineBasicMaterial({
            color: "#ffffff",
            transparent: true,
            opacity: 0.5 + Math.random() * 0.35,
          });
          const wire = new THREE.LineSegments(edges, lineMat);
          const group = new THREE.Group();
          group.add(mesh);
          group.add(wire);

          const tx = x * step;
          const ty = y * step;
          const tz = z * step;

          const angle = Math.random() * Math.PI * 2;
          const elev = (Math.random() - 0.5) * Math.PI;
          const dist = Math.random() * 40 + 22;
          const sx = Math.cos(angle) * Math.cos(elev) * dist;
          const sy = Math.sin(elev) * dist * 0.75;
          const sz = Math.sin(angle) * Math.cos(elev) * dist * 0.55 - 2;

          group.position.set(sx, sy, sz);
          scene.add(group);

          introCubes.push({
            group, sx, sy, sz, tx, ty, tz,
            rx: (Math.random() - 0.5) * 0.12,
            ry: (Math.random() - 0.5) * 0.12,
            rz: (Math.random() - 0.5) * 0.07,
            delay: (idx / 27) * 0.35,
            progress: 0,
            speed: Math.random() * 0.012 + 0.009,
          });
          idx++;
        }
      }
    }

    type ExtraCube = {
      group: THREE.Group;
      tx: number; ty: number; tz: number;
      sx: number; sy: number; sz: number;
      delay: number; progress: number; speed: number;
      rx: number; ry: number;
    };
    const extraCubes: ExtraCube[] = [];

    for (let i = 0; i < 200; i++) {
      const s = Math.random() * 0.28 + 0.07;
      const geo = new THREE.BoxGeometry(s, s, s);
      const mat = new THREE.MeshPhysicalMaterial({
        color: "#040404",
        roughness: 0.05,
        metalness: 0.1,
        clearcoat: 1,
        transparent: true,
        opacity: 0.9,
      });
      const mesh = new THREE.Mesh(geo, mat);
      const edges = new THREE.EdgesGeometry(geo);
      const lineMat = new THREE.LineBasicMaterial({
        color: "#ffffff",
        transparent: true,
        opacity: 0.4 + Math.random() * 0.45,
      });
      const wire = new THREE.LineSegments(edges, lineMat);
      const group = new THREE.Group();
      group.add(mesh);
      group.add(wire);

      const angle = Math.random() * Math.PI * 2;
      const dist = Math.random() * 38 + 10;
      const sx = Math.cos(angle) * dist;
      const sy = (Math.random() - 0.5) * dist * 0.9;
      const sz = Math.sin(angle) * dist * 0.5 - 3;
      const tx = (Math.random() - 0.5) * 2;
      const ty = (Math.random() - 0.5) * 2;
      const tz = (Math.random() - 0.5) * 2;

      group.position.set(sx, sy, sz);
      group.rotation.set(Math.random() * 6, Math.random() * 6, Math.random() * 6);
      scene.add(group);

      extraCubes.push({
        group, sx, sy, sz, tx, ty, tz,
        delay: Math.random() * 0.2,
        progress: 0,
        speed: Math.random() * 0.014 + 0.008,
        rx: (Math.random() - 0.5) * 0.1,
        ry: (Math.random() - 0.5) * 0.1,
      });
    }

    let globalT = 0;
    const TOTAL_DURATION = 0.018;
    let holdTimer = 0;
    const HOLD_FRAMES = 40;
    let fadeOpacity = 0;
    let phase: "gather" | "hold" | "fadeout" | "done" = "gather";
    let animId = 0;

    const easeOutCubic = (t: number) => 1 - Math.pow(1 - t, 3);
    const easeInQuint  = (t: number) => t * t * t * t * t;

    const shimmer = new THREE.PointLight(0xffffff, 3, 25);
    shimmer.position.set(6, 4, 8);
    scene.add(shimmer);

    const animateIntro = () => {
      animId = requestAnimationFrame(animateIntro);

      if (phase === "gather") {
        globalT = Math.min(globalT + TOTAL_DURATION, 1);
        let allDone = true;

        for (const c of introCubes) {
          const localT = Math.max(0, (globalT - c.delay) / (1 - c.delay));
          c.progress = Math.min(localT, 1);
          if (c.progress < 1) allDone = false;
          const ep = easeOutCubic(c.progress);
          c.group.position.x = c.sx + (c.tx - c.sx) * ep;
          c.group.position.y = c.sy + (c.ty - c.sy) * ep;
          c.group.position.z = c.sz + (c.tz - c.sz) * ep;
          const spin = 1 - ep;
          c.group.rotation.x += c.rx * spin;
          c.group.rotation.y += c.ry * spin;
          c.group.rotation.z += c.rz * spin;
        }

        for (const e of extraCubes) {
          const localT = Math.max(0, (globalT - e.delay) / (1 - e.delay));
          e.progress = Math.min(localT, 1);
          const ep = easeInQuint(e.progress);
          e.group.position.x = e.sx + (e.tx - e.sx) * ep;
          e.group.position.y = e.sy + (e.ty - e.sy) * ep;
          e.group.position.z = e.sz + (e.tz - e.sz) * ep;
          e.group.rotation.x += e.rx * (1 - ep);
          e.group.rotation.y += e.ry * (1 - ep);
        }

        const st = globalT * Math.PI * 4;
        shimmer.position.x = Math.cos(st) * 8;
        shimmer.position.y = Math.sin(st * 0.7) * 5;
        shimmer.position.z = Math.abs(Math.sin(st * 0.4)) * 6 + 5;

        renderer.render(scene, camera);
        if (allDone) { phase = "hold"; holdTimer = 0; }

      } else if (phase === "hold") {
        holdTimer++;
        const st = (globalT + holdTimer * 0.016) * Math.PI * 4;
        shimmer.position.x = Math.cos(st) * 8;
        shimmer.position.y = Math.sin(st * 0.7) * 5;
        shimmer.position.z = Math.abs(Math.sin(st * 0.4)) * 6 + 5;
        renderer.render(scene, camera);
        if (holdTimer >= HOLD_FRAMES) phase = "fadeout";

      } else if (phase === "fadeout") {
        fadeOpacity = Math.min(1, fadeOpacity + 0.055);
        renderer.render(scene, camera);
        if (fadeOpacity >= 1) {
          phase = "done";
          cancelAnimationFrame(animId);
          onDone();
        }
      }
    };
    animateIntro();

    return () => {
      cancelAnimationFrame(animId);
      renderer.dispose();
      if (mountRef.current && renderer.domElement.parentNode === mountRef.current) {
        mountRef.current.removeChild(renderer.domElement);
      }
    };
  }, [onDone]);

  return (
    <div
      ref={mountRef}
      className="fixed inset-0 z-50"
      style={{ background: "#000" }}
    />
  );
}

function InstagramIcon() {
  return (
    <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
      <defs>
        <radialGradient id="ig-grad" cx="30%" cy="107%" r="130%">
          <stop offset="0%" stopColor="#ffd600" />
          <stop offset="30%" stopColor="#ff7a00" />
          <stop offset="55%" stopColor="#ff0069" />
          <stop offset="80%" stopColor="#d300c5" />
          <stop offset="100%" stopColor="#7638fa" />
        </radialGradient>
      </defs>
      <rect x="2" y="2" width="20" height="20" rx="6" ry="6" stroke="url(#ig-grad)" strokeWidth="2" fill="none"/>
      <circle cx="12" cy="12" r="4.5" stroke="url(#ig-grad)" strokeWidth="2" fill="none"/>
      <circle cx="17.5" cy="6.5" r="1.2" fill="url(#ig-grad)"/>
    </svg>
  );
}

function WhatsAppIcon() {
  return (
    <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
      <circle cx="12" cy="12" r="10" stroke="#25D366" strokeWidth="2" fill="none"/>
      <path d="M17 14.9c-.2-.1-1.2-.6-1.4-.7-.2-.1-.4-.1-.5.1-.2.2-.6.7-.8.9-.1.2-.3.2-.5.1-.7-.3-1.4-.7-2-1.3-.5-.5-1-1.1-1.3-1.8-.1-.2 0-.4.1-.5l.4-.4c.1-.1.2-.3.2-.4 0-.1 0-.3-.1-.4l-.6-1.5c-.2-.4-.4-.3-.5-.3h-.4c-.2 0-.4.1-.6.3-.6.6-.9 1.3-.9 2 0 1.1.7 2.2 1.6 3.1.9.9 2 1.6 3.2 2 .4.1.8.2 1.2.2.7 0 1.4-.2 1.9-.7.3-.3.5-.7.5-1.1 0-.2-.1-.3-.2-.3z" fill="#25D366"/>
    </svg>
  );
}

type GlassButtonProps = {
  icon: React.ReactNode;
  label: string;
  sublabel: string;
};

function GlassButton({ icon, label, sublabel }: GlassButtonProps) {
  return (
    <div
      className="w-full flex items-center gap-3 px-5 py-3 transition-all duration-200 active:scale-95 hover:scale-[1.02]"
      style={{
        background: "rgba(255,255,255,0.055)",
        border: "1px solid rgba(255,255,255,0.22)",
        borderRadius: "50px 18px 18px 50px",
        backdropFilter: "blur(18px) saturate(1.4)",
        WebkitBackdropFilter: "blur(18px) saturate(1.4)",
        boxShadow: "inset 0 1px 0 rgba(255,255,255,0.12), inset 0 -1px 0 rgba(255,255,255,0.04), 0 4px 24px rgba(0,0,0,0.35)",
      }}
    >
      <div className="flex-shrink-0 w-8 h-8 flex items-center justify-center">
        {icon}
      </div>
      <div className="flex flex-col leading-tight">
        <span className="text-white font-semibold text-sm tracking-wide" style={{ textShadow: "0 1px 4px rgba(0,0,0,0.5)" }}>
          {label}
        </span>
        <span className="text-white/50 text-xs font-light tracking-wide">{sublabel}</span>
      </div>
    </div>
  );
}

export default function Index() {
  const [showIntro, setShowIntro] = React.useState(true);

  return (
    <div
      className="min-h-screen w-full flex flex-col items-center justify-start overflow-x-hidden"
      style={{ background: "#000000" }}
    >
      {showIntro && (
        <IntroAnimation onDone={() => setShowIntro(false)} />
      )}
      <StarField />
      <div
        className="fixed inset-0 pointer-events-none"
        style={{
          background: "radial-gradient(ellipse 60% 40% at 50% 0%, rgba(255,255,255,0.03) 0%, transparent 70%)",
        }}
      />

      <div className="relative z-10 flex flex-col items-center w-full px-4 pt-14 pb-12">

        {/* Name with animated aurora */}
        <motion.div
          initial={{ opacity: 0, y: -28 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.9, ease: "easeOut" }}
          className="relative flex items-center justify-center px-8 py-4"
        >
          <motion.div
            className="absolute pointer-events-none"
            style={{
              width: "160%", height: "400%", top: "-150%", left: "-30%",
              background: "radial-gradient(ellipse 90% 18% at 50% 50%, rgba(0,255,80,0.9) 0%, rgba(0,255,80,0.4) 40%, transparent 70%)",
              filter: "blur(12px)",
            }}
            animate={{
              x: [-30, 30, -15, 40, -30], y: [-20, 20, -30, 10, -20],
              scaleX: [1, 1.5, 0.7, 1.3, 1], scaleY: [1, 0.6, 1.4, 0.8, 1],
              opacity: [0.9, 1, 0.7, 1, 0.9], rotate: [-8, 5, -12, 8, -8],
            }}
            transition={{ duration: 4, repeat: Infinity, ease: "easeInOut" }}
          />
          <motion.div
            className="absolute pointer-events-none"
            style={{
              width: "140%", height: "350%", top: "-120%", left: "-20%",
              background: "radial-gradient(ellipse 85% 12% at 50% 40%, rgba(0,220,180,0.85) 0%, rgba(0,255,150,0.35) 45%, transparent 70%)",
              filter: "blur(10px)",
            }}
            animate={{
              x: [30, -20, 40, -30, 30], y: [10, -25, 15, -18, 10],
              scaleX: [0.8, 1.6, 0.9, 1.4, 0.8], scaleY: [1.3, 0.5, 1.5, 0.7, 1.3],
              opacity: [0.8, 1, 0.6, 0.95, 0.8], rotate: [6, -10, 14, -6, 6],
            }}
            transition={{ duration: 5, repeat: Infinity, ease: "easeInOut", delay: 0.8 }}
          />
          <motion.div
            className="absolute pointer-events-none"
            style={{
              width: "180%", height: "300%", top: "-100%", left: "-40%",
              background: "radial-gradient(ellipse 95% 8% at 50% 60%, rgba(100,255,120,0.95) 0%, rgba(0,255,80,0.3) 50%, transparent 70%)",
              filter: "blur(8px)",
            }}
            animate={{
              x: [-40, 35, -25, 45, -40], y: [-5, 20, -25, 12, -5],
              scaleX: [1.1, 0.6, 1.4, 0.8, 1.1], scaleY: [1, 1.8, 0.6, 1.5, 1],
              opacity: [1, 0.6, 0.9, 0.7, 1], rotate: [-14, 10, -18, 6, -14],
            }}
            transition={{ duration: 6, repeat: Infinity, ease: "easeInOut", delay: 0.3 }}
          />
          <motion.div
            className="absolute pointer-events-none"
            style={{
              width: "150%", height: "320%", top: "-130%", left: "-25%",
              background: "radial-gradient(ellipse 80% 10% at 50% 45%, rgba(0,180,255,0.7) 0%, rgba(60,255,180,0.25) 50%, transparent 72%)",
              filter: "blur(14px)",
            }}
            animate={{
              x: [20, -35, 28, -22, 20], y: [15, -12, 22, -18, 15],
              scaleX: [0.9, 1.5, 0.75, 1.3, 0.9], scaleY: [1.2, 0.5, 1.6, 0.7, 1.2],
              opacity: [0.7, 1, 0.5, 0.85, 0.7], rotate: [10, -8, 16, -12, 10],
            }}
            transition={{ duration: 7, repeat: Infinity, ease: "easeInOut", delay: 1.5 }}
          />
          <motion.div
            className="absolute pointer-events-none"
            style={{
              width: "200%", height: "260%", top: "-80%", left: "-50%",
              background: "radial-gradient(ellipse 100% 5% at 50% 55%, rgba(180,255,200,0.9) 0%, rgba(0,255,80,0.2) 55%, transparent 72%)",
              filter: "blur(6px)",
            }}
            animate={{
              x: [-50, 40, -30, 50, -50], y: [0, -15, 25, -10, 0],
              scaleX: [1, 0.5, 1.3, 0.7, 1], opacity: [0.8, 0.4, 1, 0.5, 0.8],
              rotate: [-5, 12, -20, 8, -5],
            }}
            transition={{ duration: 5.5, repeat: Infinity, ease: "easeInOut", delay: 2 }}
          />

          <h1
            className="relative text-3xl md:text-4xl font-bold tracking-[0.18em] uppercase whitespace-nowrap select-none"
            style={{
              fontFamily: "'Rajdhani', 'Geist', ui-sans-serif, system-ui",
              color: "#ffffff",
              textShadow: "0 0 2px rgba(255,255,255,0.9), 0 0 8px rgba(0,255,80,0.4)",
              zIndex: 10,
            }}
          >
            Pirro Skapeta
          </h1>
        </motion.div>

        {/* Subtitle */}
        <motion.div
          initial={{ opacity: 0, y: 10 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.9, delay: 0.18, ease: "easeOut" }}
          className="flex items-center gap-2 mt-2 mb-8"
        >
          <span style={{ color: "#FFD700", fontSize: "14px", lineHeight: 1 }}>★</span>
          <p
            className="text-xs md:text-sm tracking-[0.12em] font-light"
            style={{
              fontFamily: "'Rajdhani', ui-sans-serif, system-ui",
              color: "rgba(255,255,255,0.75)",
              textShadow: "0 0 8px rgba(255,255,255,0.5), 0 0 20px rgba(255,255,255,0.2)",
            }}
          >
            {"i'm owner of the "}
            <span style={{ textTransform: "uppercase", fontWeight: 600, color: "rgba(255,255,255,0.95)" }}>
              Skapeta Apartments
            </span>
          </p>
          <span style={{ color: "#FFD700", fontSize: "14px", lineHeight: 1 }}>★</span>
        </motion.div>

        {/* Rubik's Cube */}
        <motion.div
          initial={{ opacity: 0, scale: 0.82 }}
          animate={{ opacity: 1, scale: 1 }}
          transition={{ duration: 1.1, delay: 0.3, ease: "easeOut" }}
          className="flex items-center justify-center"
        >
          <RubiksCube />
        </motion.div>

        {/* Buttons */}
        <motion.div
          initial={{ opacity: 0, y: 28 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.85, delay: 0.55, ease: "easeOut" }}
          className="flex flex-col items-center gap-3 mt-8 w-full max-w-xs"
        >
          <a href="https://instagram.com/pirro_skapeta" target="_blank" rel="noopener noreferrer" className="w-full cursor-pointer">
            <GlassButton icon={<InstagramIcon />} label="Instagram" sublabel="@pirro_skapeta" />
          </a>
          <a href="https://instagram.com/skapetaapartments" target="_blank" rel="noopener noreferrer" className="w-full cursor-pointer">
            <GlassButton icon={<InstagramIcon />} label="Instagram" sublabel="@skapetaapartments" />
          </a>
          <a href="https://wa.me/355693227207" target="_blank" rel="noopener noreferrer" className="w-full cursor-pointer">
            <GlassButton icon={<WhatsAppIcon />} label="WhatsApp" sublabel="+355 69 322 7207" />
          </a>
        </motion.div>
      </div>
    </div>
  );
}
