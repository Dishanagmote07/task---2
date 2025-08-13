# task---2
ui ux design
"use client";

import { icons, LucideProps, type LucideIcon as LucideIconType } from 'lucide-react';
import { createElement, useMemo } from 'react';

const FallbackIcon: LucideIconType = icons['ListTodo'];

const toPascalCase = (str: string) => {
  if (!str) return '';
  return str
    .replace(/[-_.\s]+(.)?/g, (_match, c) => c ? c.toUpperCase() : '')
    .replace(/^./, (c) => c.toUpperCase());
};

interface IconRendererProps extends LucideProps {
  name: string;
}

export const IconRenderer = ({ name, ...props }: IconRendererProps) => {
  const IconComponent = useMemo(() => {
    const pascalCaseName = toPascalCase(name);
    const foundIcon = icons[pascalCaseName as keyof typeof icons];
    return foundIcon || FallbackIcon;
  }, [name]);

  return createElement(IconComponent, props);
};
