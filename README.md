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