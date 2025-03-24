"use client";

import React from "react";
import Link from "next/link";
import Image from "next/image";
import { Button } from "@/components/ui/button";

export interface ProductItemProps {
  title: string;
  subtitle: string;
  description?: string;
  backgroundImage: string;
  logo?: string;
  textColor?: "dark" | "light";
  learnMoreLink?: string;
  buyLink?: string;
}

function ProductItem({
  title,
  subtitle,
  description,
  backgroundImage,
  logo,
  textColor = "dark",
  learnMoreLink = "#",
  buyLink = "#",
}: ProductItemProps) {
  const textColorClass = textColor === "dark" ? "text-[#1d1d1f]" : "text-white";

  return (
    <div
      className="flex flex-col items-center justify-center bg-cover bg-center relative h-[490px] md:h-[580px] rounded-2xl overflow-hidden"
      style={{ backgroundImage: `url(${backgroundImage})` }}
    >
      <div className="text-center z-10 px-6 flex flex-col items-center">
        {logo ? (
          <Image
            src={logo}
            alt={title}
            width={120}
            height={48}
            className="mb-4"
          />
        ) : (
          <h3 className={`text-3xl md:text-4xl font-semibold mb-1 ${textColorClass}`}>
            {title}
          </h3>
        )}
        <p className={`text-xl md:text-2xl mb-2 ${textColorClass}`}>
          {subtitle}
        </p>
        {description && (
          <p className={`text-sm max-w-md mb-4 ${textColorClass}`}>
            {description}
          </p>
        )}
        <div className="flex items-center justify-center gap-4 mt-3">
          <Link href={learnMoreLink}>
            <Button
              variant="link"
              className={`${textColorClass} text-base font-normal hover:underline`}
            >
              Learn more &gt;
            </Button>
          </Link>
          <Link href={buyLink}>
            <Button
              variant="link"
              className={`${textColorClass} text-base font-normal hover:underline`}
            >
              Buy &gt;
            </Button>
          </Link>
        </div>
      </div>
    </div>
  );
}

interface ProductGridProps {
  products: ProductItemProps[];
}

export default function ProductGrid({ products }: ProductGridProps) {
  return (
    <div className="grid grid-cols-1 md:grid-cols-2 gap-3 px-3 my-3">
      {products.map((product, index) => (
        <ProductItem key={index} {...product} />
      ))}
    </div>
  );
}
