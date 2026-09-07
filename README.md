# Bruno---virtual-pet
Bruno – My Virtual Pet | An interactive virtual dog that you can feed, play with, clean, dress, and care for. Currently a prototype and open to improvements.

#  Bruno – My Virtual Pet

Bruno is a virtual pet dog project where users can take care of their own virtual companion.

## Current Features

-  Feed Bruno
-  Play with Bruno
-  Clean Bruno
-  Dress Bruno
-  Change owner name
-  Pet stats and interactions

## Project Status

This is an early prototype and is still under development.

## What I Want to Build

I want Bruno to become a much more interactive virtual pet, inspired by the experience of classic virtual-pet games.

Future ideas include:

- Talking and voice interactions
- Real-time facial/emotional reactions
- More realistic pet animations
- Mini-games
- A larger wardrobe
- A customizable room
- Pet personality and memory
- Sounds and voice responses
- A polished mobile-app experience

 artifacts/bruno-virtual-=====pet/src/App.tsx ==artifacts===
import { type PointerEvent asartifactsartifacts ReactPointerEvent, useEffect, useMemo, useState } from 'react';
import { Check, ChevronRight, CircleUserRound, Droplets, Heart, Home, MoreHorizontal, PawPrint, Pencil, RotateCcw, Save, Settings, Shirt, X } from 'lucide-react';

type View = 'home' | 'wardrobe' | 'settings';
type OutfitId = 'classic' | 'rainy' | 'sailor' | 'sleepy' | 'flower';
type StatKey = 'hunger' | 'happiness' | 'cleanliness' | 'energy';
type PetEmotion = 'idle' | 'laugh' | 'cry' | 'angry' | 'bark' | 'clean';
type OpenPanel = 'food' | 'bath' | null;
type BathStep = 'soap' | 'rinse';

type Stats = Record<StatKey, number>;
type Outfit = {
  id: OutfitId;
  name: string;
  emoji: string;
  description: string;
  tint: string;
  sticker: string;
  stickerClass: string;
};
type Dish = {
  id: string;
  name: string;
  emoji: string;
  detail: string;
  boost: number;
  tint: string;
};

const STORAGE_KEY = 'bruno-virtual-pet-v1';
const defaultStats: Stats = { hunger: 58, happiness: 78, cleanliness: 64, energy: 71 };

const outfits: Outfit[] = [


id: 'classic', name: 'Red bandana', emoji: '🎀', description: 'Bruno’s signature look', tint: '#f7d8cf', sticker: '🎀', stickerClass: 'sticker-bandana' },
  { id: 'rainy', name: 'Rainy day', emoji: '🌧️', description: 'Ready for puddle walks', tint: '#d7e9e8', sticker: '🧢', stickerClass: 'sticker-cap' },
  { id: 'sailor', name: 'Little sailor', emoji: '⚓', description: 'All aboard for cuddles', tint: '#dce5f0', sticker: '⚓', stickerClass: 'sticker-sailor' },
  { id: 'sleepy', name: 'Cozy dreamer', emoji: '🌙', description: 'Soft paws, softer naps', tint: '#e9e0ef', sticker: '🌙', stickerClass: 'sticker-moon' },
  { id: 'flower', name: 'Garden pup', emoji: '🌼', description: 'A little sunshine', tint: '#f1e4b4', sticker: '🌼', stickerClass: 'sticker-flower' },
];
const dishes: Dish[] = [
  { id: 'kibble', name: 'Puppy kibble', emoji: '🥣', detail: 'His everyday favorite', boost: 18, tint: '#f2dfc1' },
  { id: 'chicken', name: 'Chicken bites', emoji: '🍗', detail: 'Tiny, tasty pieces', boost: 24, tint: '#f4c6b7' },
  { id: 'pancakes', name: 'Pup pancakes', emoji: '🥞', detail: 'A weekend treat', boost: 28, tint: '#e9d6a9' },
className="rounded-full bg-[#fff6d7] px-2 py-1 text-[10px] font-bold uppercase tracking-wider">Today</span>
            </div>
            <p className="font-serif text-lg leading-tight">Small rituals,<br />big tail wags.</p>
            <p className="mt-2 text-xs leading-relaxed text-[#806741]">Bruno is here whenever you need a soft hello.</p>
          </div>
        </aside>

        <main className="min-w-0 flex-1">
          <header className="flex items-center justify-between px-5 pb-2 pt-6 sm:px-8 md:px-12 md:pt-9">
            <div className="flex items-center gap-3 md:hidden"><Logo compact /></div>
            <div className="hidden md:block">
               <p className="text-sm font-semibold text-muted-foreground">{new Intl.DateTimeFormat('en-US', { weekday: 'long', month: 'long', day: 'numeric' }).format(new Date())}</p>
              <h1 className="mt-1 font-serif text-3xl text-foreground">{view === 'home' ? 'A good day starts here.' : view === 'wardrobe' ? 'Bruno’s closet.' : 'A little care goes a long way.'}</h1>
            </div>
            <div className="flex items-center gap-2">
              <div className="hidden items-center gap-2 rounded-full bg-[hsl(var(--card))] px-3 py-2 text-xs font-semibold text-muted-foreground shadow-sm sm:flex">
                <span className="h-2 w-2 rounded-full bg-[#7fb8a8]" />
                Saved locally
              </div>
              <button aria-label="More options" data-testid="button-more-options" className="rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}rounded-full p-2 text-muted-foreground transition hover:bg-[hsl(var(--muted))]"><MoreHorizontal size={21} /></button>
            </div>
          </header>

          <div className="px-5 pb-28 pt-5 sm:px-8 md:px-12 md:pb-12 md:pt-8">
            {view === 'home' && (
              <HomeView
                greetingName={greetingName}
                stats={stats}
                message={message}
                emotion={mood}
                activeOutfit={activeOutfit}
                lastAction={lastAction}
                onFeed={openFoodTray}
                onPlay={() => doAction('play')}
                onClean={openBath}
                onDress={() => setView('wardrobe')}
                onSettings={() => setView('settings')}
                onTouch={touchPuppy}
                onScratch={scratchPuppy}
              />
            )}
            {view === 'wardrobe' && (
              <WardrobeView outfit={outfit} activeOutfit={activeOutfit} onChoose={chooseOutfit} onBack={() => setView('home')} />
            )}
            {view === 'settings' && (
              <SettingsView
                ownerName={ownerName}
                draftName={draftName}