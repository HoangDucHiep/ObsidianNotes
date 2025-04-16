Tiếp theo là các code phần API:
namespace FlashcardApi.Application.Card.Dtos;

public class CardDto
{
    public string? Id { get; set; }
    public string DeskId { get; set; }
    public string Front { get; set; }
    public string Back { get; set; }
    public List<string> ImagePaths { get; set; } = new List<string>(); // Danh sách tên file ảnh
    public DateTime CreatedAt { get; set; }
    public DateTime LastModified { get; set; }
}

namespace FlashcardApi.Application.Desk.Dtos;

public class DeskDto
{
    public string? Id { get; set; }
    public string Name { get; set; }
    public bool IsPublic { get; set; }
    public string? FolderId { get; set; }
    public DateTime CreatedAt { get; set; }
    public DateTime LastModified { get; set; }
}

namespace FlashcardApi.Application.Folder.Dtos;

public class FolderDto
{
    public string? Id { get; set; }
    public string Name { get; set; }
    public string? ParentFolderId { get; set; }
    public DateTime CreatedAt { get; set; }
    public DateTime LastModified { get; set; }
}

namespace FlashcardApi.Application.Image.Dtos;

public class ImageDto
{
    public string? Id { get; set; }
    public string FileName { get; set; }
    public string Url { get; set; }
    public DateTime UploadedAt { get; set; }
}

namespace FlashcardApi.Application.Review.Dtos;

public class ReviewDto
{
    public string? Id { get; set; } // Nullable cho POST
    public string CardId { get; set; }
    public double Ease { get; set; }
    public int Interval { get; set; }
    public int Repetition { get; set; }
    public string NextReviewDate { get; set; }
    public string? LastReviewed { get; set; }
}



namespace FlashcardApi.Application.Session.Dtos;

public class SessionDto
{
    public string? Id { get; set; } // Nullable cho POST
    public string DeskId { get; set; }
    public string StartTime { get; set; }
    public string? EndTime { get; set; }
    public int CardsStudied { get; set; }
    public double Performance { get; set; }
}

using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;
using FlashcardApi.Infrastructure.Persistence;
using Microsoft.EntityFrameworkCore;

namespace FlashcardApi.Infrastructure.Repositories;

public class CardRepository : ICardRepository
{
    private readonly AppDbContext _context;

    public CardRepository(AppDbContext context)
    {
        _context = context;
    }

    public async Task<List<Card>> GetByDeskIdAsync(string deskId)
    {
        return await _context.Cards.Where(c => c.DeskId == deskId).ToListAsync();
    }

    public async Task<Card> GetByIdAsync(string id)
    {
        return await _context.Cards.FindAsync(id);
    }

    public async Task AddAsync(Card card)
    {
        await _context.Cards.AddAsync(card);
        await _context.SaveChangesAsync();
    }

    public async Task UpdateAsync(Card card)
    {
        _context.Cards.Update(card);
        await _context.SaveChangesAsync();
    }

    public async Task DeleteAsync(string id)
    {
        var card = await GetByIdAsync(id);
        if (card != null)
        {
            _context.Cards.Remove(card);
            await _context.SaveChangesAsync();
        }
    }
}

using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;
using FlashcardApi.Infrastructure.Persistence;
using Microsoft.EntityFrameworkCore;

namespace FlashcardApi.Infrastructure.Repositories;

public class DeskRepository : IDeskRepository
{
    private readonly AppDbContext _context;

    public DeskRepository(AppDbContext context)
    {
        _context = context;
    }

    public async Task<List<Desk>> GetByOwnerIdAsync(string ownerId)
    {
        return await _context.Desks.Where(d => d.OwnerId == ownerId).ToListAsync();
    }

    public async Task<List<Desk>> GetPublicDesksAsync()
    {
        return await _context.Desks.Where(d => d.IsPublic).ToListAsync();
    }

    public async Task<Desk> GetByIdAsync(string id)
    {
        return await _context.Desks.FindAsync(id);
    }

    public async Task AddAsync(Desk desk)
    {
        await _context.Desks.AddAsync(desk);
        await _context.SaveChangesAsync();
    }

    public async Task UpdateAsync(Desk desk)
    {
        _context.Desks.Update(desk);
        await _context.SaveChangesAsync();
    }

    public async Task DeleteAsync(string id)
    {
        var desk = await GetByIdAsync(id);
        if (desk != null)
        {
            _context.Desks.Remove(desk);
            await _context.SaveChangesAsync();
        }
    }
}

using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;
using FlashcardApi.Infrastructure.Persistence;
using Microsoft.EntityFrameworkCore;

namespace FlashcardApi.Infrastructure.Repositories;

public class FolderRepository : IFolderRepository
{
    private readonly AppDbContext _context;

    public FolderRepository(AppDbContext context)
    {
        _context = context;
    }

    public async Task<List<Folder>> GetByOwnerIdAsync(string ownerId)
    {
        return await _context.Folders.Where(f => f.OwnerId == ownerId).ToListAsync();
    }

    public async Task<Folder> GetByIdAsync(string id)
    {
        return await _context.Folders.FindAsync(id);
    }

    public async Task AddAsync(Folder folder)
    {
        await _context.Folders.AddAsync(folder);
        await _context.SaveChangesAsync();
    }

    public async Task UpdateAsync(Folder folder)
    {
        _context.Folders.Update(folder);
        await _context.SaveChangesAsync();
    }

    public async Task DeleteAsync(string id)
    {
        var folder = await GetByIdAsync(id);
        if (folder != null)
        {
            _context.Folders.Remove(folder);
            await _context.SaveChangesAsync();
        }
    }
}

using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;
using FlashcardApi.Infrastructure.Persistence;
using Microsoft.EntityFrameworkCore;

namespace FlashcardApi.Infrastructure.Repositories;

public class ImageRepository : IImageRepository
{
    private readonly AppDbContext _context;

    public ImageRepository(AppDbContext context)
    {
        _context = context;
    }

    public async Task<Image> AddAsync(Image image)
    {
        await _context.Images.AddAsync(image);
        await _context.SaveChangesAsync();
        return image;
    }

    public async Task DeleteAsync(string id)
    {
        var image = await _context.Images.FindAsync(id);
        if (image != null)
        {
            _context.Images.Remove(image);
            await _context.SaveChangesAsync();
        }
    }

    public async Task<Image> GetByFileNameAsync(string fileName)
    {
        return await _context.Images.FirstOrDefaultAsync(i => i.Url.EndsWith(fileName));
    }

    public async Task<List<Image>> GetAllAsync()
    {
        return await _context.Images.ToListAsync();
    }
}


using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;
using FlashcardApi.Infrastructure.Persistence;
using Microsoft.EntityFrameworkCore;

namespace FlashcardApi.Infrastructure.Repositories;

public class ReviewRepository : IReviewRepository
{
    private readonly AppDbContext _context;

    public ReviewRepository(AppDbContext context)
    {
        _context = context;
    }

    public async Task<Review> CreateAsync(Review review)
    {
        await _context.Reviews.AddAsync(review);
        await _context.SaveChangesAsync();
        return review;
    }

    public async Task<Review> UpdateAsync(Review review)
    {
        _context.Reviews.Update(review);
        await _context.SaveChangesAsync();
        return review;
    }

    public async Task DeleteAsync(string id)
    {
        var review = await _context.Reviews.FindAsync(id);
        if (review != null)
        {
            _context.Reviews.Remove(review);
            await _context.SaveChangesAsync();
        }
    }

    public async Task<Review> GetByCardIdAsync(string cardId)
    {
        return await _context.Reviews.FirstOrDefaultAsync(r => r.CardId == cardId);
    }

    public async Task<List<Review>> GetReviewsDueTodayAsync(string deskId, string today)
    {
        return await _context
            .Reviews.Join(
                _context.Cards,
                r => r.CardId,
                c => c.Id,
                (r, c) => new { Review = r, Card = c }
            )
            .Where(rc => rc.Card.DeskId == deskId && rc.Review.NextReviewDate.CompareTo(today) <= 0)
            .Select(rc => rc.Review)
            .ToListAsync();
    }
}

using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;
using FlashcardApi.Infrastructure.Persistence;
using Microsoft.EntityFrameworkCore;

namespace FlashcardApi.Infrastructure.Repositories;

public class SessionRepository : ISessionRepository
{
    private readonly AppDbContext _context;

    public SessionRepository(AppDbContext context)
    {
        _context = context;
    }

    public async Task<Session> CreateAsync(Session session)
    {
        await _context.Sessions.AddAsync(session);
        await _context.SaveChangesAsync();
        return session;
    }

    public async Task<Session> UpdateAsync(Session session)
    {
        _context.Sessions.Update(session);
        await _context.SaveChangesAsync();
        return session;
    }

    public async Task DeleteAsync(string id)
    {
        var session = await _context.Sessions.FindAsync(id);
        if (session != null)
        {
            _context.Sessions.Remove(session);
            await _context.SaveChangesAsync();
        }
    }

    public async Task<List<Session>> GetByDeskIdAsync(string deskId)
    {
        return await _context.Sessions.Where(s => s.DeskId == deskId).ToListAsync();
    }
}


using System.IdentityModel.Tokens.Jwt;
using System.Security.Claims;
using System.Text;
using FlashcardApi.Application.ApplicationUser;
using FlashcardApi.Application.ApplicationUser.Dtos;
using FlashcardApi.Domain.Entities;
using Microsoft.AspNetCore.Identity;
using Microsoft.Extensions.Configuration;
using Microsoft.IdentityModel.Tokens;

namespace FlashcardApi.Infrastructure.Services;

public class AuthService : IAuthService
{
    private readonly UserManager<ApplicationUser> _userManager;
    private readonly IConfiguration _configuration;
    private readonly IRevokedTokenRepository _revokedTokenRepository;

    public AuthService(
        UserManager<ApplicationUser> userManager,
        IConfiguration configuration,
        IRevokedTokenRepository revokedTokenRepository
    )
    {
        _userManager = userManager;
        _configuration = configuration;
        _revokedTokenRepository = revokedTokenRepository;
    }

    public async Task<LoginResponseDto> LoginAsync(LoginRequestDto request)
    {
        var user = await _userManager.FindByNameAsync(request.Username);
        if (user == null || !await _userManager.CheckPasswordAsync(user, request.Password))
            throw new Exception("Invalid credentials");

        // Thu hồi token cũ nếu tồn tại
        if (!string.IsNullOrEmpty(user.CurrentToken))
        {
            await _revokedTokenRepository.AddAsync(
                new RevokedToken
                {
                    Token = user.CurrentToken,
                    ExpiresAt = DateTime.UtcNow.AddYears(1), // Hoặc thời gian hợp lệ
                }
            );
        }

        // Tạo token mới
        var token = GenerateJwtToken(user);

        // Lưu token mới vào bảng người dùng
        user.CurrentToken = token;
        await _userManager.UpdateAsync(user);

        return new LoginResponseDto { Token = token, Username = user.UserName };
    }

    public async Task LogoutAsync(string token)
    {
        var handler = new JwtSecurityTokenHandler();
        var jwtToken = handler.ReadJwtToken(token);
        var userId = jwtToken.Claims.First(c => c.Type == ClaimTypes.NameIdentifier).Value;

        var user = await _userManager.FindByIdAsync(userId);
        if (user != null && user.CurrentToken == token)
        {
            // Thu hồi token
            await _revokedTokenRepository.AddAsync(
                new RevokedToken { Token = token, ExpiresAt = jwtToken.ValidTo }
            );

            // Xóa token khỏi bảng người dùng
            user.CurrentToken = null;
            await _userManager.UpdateAsync(user);
        }
    }

    public async Task RegisterAsync(string username, string password)
    {
        var user = new ApplicationUser { UserName = username, Email = username + "@example.com" };
        var result = await _userManager.CreateAsync(user, password);
        if (!result.Succeeded)
            throw new Exception(
                "Registration failed: "
                    + string.Join(", ", result.Errors.Select(e => e.Description))
            );
    }

    private string GenerateJwtToken(ApplicationUser user)
    {
        var claims = new[]
        {
            new Claim(ClaimTypes.NameIdentifier, user.Id),
            new Claim(ClaimTypes.Name, user.UserName),
        };

        var key = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(_configuration["Jwt:Key"]));
        var creds = new SigningCredentials(key, SecurityAlgorithms.HmacSha256);
        var token = new JwtSecurityToken(
            issuer: _configuration["Jwt:Issuer"],
            audience: _configuration["Jwt:Audience"],
            claims: claims,
            expires: DateTime.Now.AddDays(1),
            signingCredentials: creds
        );

        return new JwtSecurityTokenHandler().WriteToken(token);
    }
}

using System.Text.RegularExpressions;
using FlashcardApi.Application.Card;
using FlashcardApi.Application.Card.Dtos;
using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;

namespace FlashcardApi.Infrastructure.Services;

public class CardService : ICardService
{
    private readonly ICardRepository _cardRepository;
    private readonly IImageRepository _imageRepository;

    public CardService(ICardRepository cardRepository, IImageRepository imageRepository)
    {
        _cardRepository = cardRepository;
        _imageRepository = imageRepository;
    }

    public async Task<List<CardDto>> GetCardsByDeskIdAsync(string deskId)
    {
        var cards = await _cardRepository.GetByDeskIdAsync(deskId);
        return cards
            .Select(c => new CardDto
            {
                Id = c.Id,
                DeskId = c.DeskId,
                Front = c.Front,
                Back = c.Back,
                ImagePaths = ExtractImagePaths(c.Front, c.Back), // Trích xuất từ HTML
                CreatedAt = c.CreatedAt,
                LastModified = c.LastModified,
            })
            .ToList();
    }

    public async Task<CardDto> CreateCardAsync(CardDto cardDto)
    {
        var card = new Card
        {
            DeskId = cardDto.DeskId,
            Front = cardDto.Front,
            Back = cardDto.Back,
        };
        await _cardRepository.AddAsync(card);
        return new CardDto
        {
            Id = card.Id,
            DeskId = card.DeskId,
            Front = card.Front,
            Back = card.Back,
            ImagePaths = cardDto.ImagePaths, // Giữ nguyên danh sách từ client
            CreatedAt = card.CreatedAt,
            LastModified = card.LastModified,
        };
    }

    public async Task<CardDto> UpdateCardAsync(string id, CardDto cardDto)
    {
        var card = await _cardRepository.GetByIdAsync(id);
        if (card == null)
            throw new Exception("Card not found");

        card.Front = cardDto.Front;
        card.Back = cardDto.Back;
        card.LastModified = DateTime.UtcNow;

        await _cardRepository.UpdateAsync(card);
        return new CardDto
        {
            Id = card.Id,
            DeskId = card.DeskId,
            Front = card.Front,
            Back = card.Back,
            ImagePaths = cardDto.ImagePaths, // Giữ nguyên danh sách từ client
            CreatedAt = card.CreatedAt,
            LastModified = card.LastModified,
        };
    }

    public async Task DeleteCardAsync(string id)
    {
        var card = await _cardRepository.GetByIdAsync(id);
        if (card == null)
            throw new Exception("Card not found");

        await _cardRepository.DeleteAsync(id);
    }

    public async Task CleanupUnusedImagesAsync(string deskId, List<string> usedImagePaths)
    {
        var allCards = await _cardRepository.GetByDeskIdAsync(deskId);
        var allUsedImagePaths = new HashSet<string>();

        // Thu thập tất cả ảnh đang dùng trong Desk
        foreach (var card in allCards)
        {
            var imagePaths = ExtractImagePaths(card.Front, card.Back);
            allUsedImagePaths.UnionWith(imagePaths);
        }

        // Xác định ảnh không còn dùng
        var allImages = await _imageRepository.GetAllAsync(); // Giả định có phương thức này
        foreach (var image in allImages)
        {
            string fileName = Path.GetFileName(image.Url);
            if (!allUsedImagePaths.Contains(fileName))
            {
                await _imageRepository.DeleteAsync(image.Id);
            }
        }
    }

    private List<string> ExtractImagePaths(string front, string back)
    {
        var imagePaths = new List<string>();
        string combinedHtml = (front ?? "") + (back ?? "");
        var matches = Regex.Matches(combinedHtml, @"<img[^>]+src=[""'](.*?)[""'][^>]*>");
        foreach (Match match in matches) // Chỉ định kiểu Match thay vì var
        {
            string src = match.Groups[1].Value; // Groups[1] là phần trong dấu ngoặc đơn của regex
            string fileName = Path.GetFileName(src);
            if (!string.IsNullOrEmpty(fileName))
                imagePaths.Add(fileName);
        }
        return imagePaths;
    }
}


using FlashcardApi.Application.Desk;
using FlashcardApi.Application.Desk.Dtos;
using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;

namespace FlashcardApi.Infrastructure.Services;

public class DeskService : IDeskService
{
    private readonly IDeskRepository _deskRepository;
    private readonly ICardRepository _cardRepository;

    public DeskService(IDeskRepository deskRepository, ICardRepository cardRepository)
    {
        _deskRepository = deskRepository;
        _cardRepository = cardRepository;
    }

    public async Task<List<DeskDto>> GetUserDesksAsync(string userId)
    {
        var desks = await _deskRepository.GetByOwnerIdAsync(userId);
        return desks
            .Select(d => new DeskDto
            {
                Id = d.Id,
                Name = d.Name,
                IsPublic = d.IsPublic,
                FolderId = d.FolderId,
                CreatedAt = d.CreatedAt,
                LastModified = d.LastModified,
            })
            .ToList();
    }

    public async Task<List<DeskDto>> GetPublicDesksAsync()
    {
        var desks = await _deskRepository.GetPublicDesksAsync();
        return desks
            .Select(d => new DeskDto
            {
                Id = d.Id,
                Name = d.Name,
                IsPublic = d.IsPublic,
                FolderId = d.FolderId,
                CreatedAt = d.CreatedAt,
                LastModified = d.LastModified,
            })
            .ToList();
    }

    public async Task<DeskDto> CreateDeskAsync(string userId, DeskDto deskDto)
    {
        var desk = new Desk
        {
            OwnerId = userId,
            Name = deskDto.Name,
            IsPublic = deskDto.IsPublic,
            FolderId = deskDto.FolderId,
        };
        await _deskRepository.AddAsync(desk);
        return new DeskDto
        {
            Id = desk.Id,
            Name = desk.Name,
            IsPublic = desk.IsPublic,
            FolderId = desk.FolderId,
            CreatedAt = desk.CreatedAt,
            LastModified = desk.LastModified,
        };
    }

    public async Task<DeskDto> UpdateDeskAsync(string id, DeskDto deskDto)
    {
        var desk = await _deskRepository.GetByIdAsync(id);
        if (desk == null)
            throw new Exception("Desk not found");

        desk.Name = deskDto.Name;
        desk.IsPublic = deskDto.IsPublic;
        desk.FolderId = deskDto.FolderId;
        desk.LastModified = DateTime.UtcNow;

        await _deskRepository.UpdateAsync(desk);
        return new DeskDto
        {
            Id = desk.Id,
            Name = desk.Name,
            IsPublic = desk.IsPublic,
            FolderId = desk.FolderId,
            CreatedAt = desk.CreatedAt,
            LastModified = desk.LastModified,
        };
    }

    public async Task DeleteDeskAsync(string id)
    {
        var desk = await _deskRepository.GetByIdAsync(id);
        if (desk == null)
            throw new Exception("Desk not found");

        await _deskRepository.DeleteAsync(id);
    }

    public async Task<DeskDto> CloneDeskAsync(string userId, string deskId)
    {
        var originalDesk = await _deskRepository.GetByIdAsync(deskId);
        if (originalDesk == null)
            throw new Exception("Desk not found");

        var clonedDesk = new Desk
        {
            OwnerId = userId,
            Name = originalDesk.Name + " (Cloned)",
            IsPublic = false, // Mặc định không công khai
            FolderId = originalDesk.FolderId,
        };
        await _deskRepository.AddAsync(clonedDesk);

        var cards = await _cardRepository.GetByDeskIdAsync(deskId);
        foreach (var card in cards)
        {
            var clonedCard = new Card
            {
                DeskId = clonedDesk.Id,
                Front = card.Front,
                Back = card.Back,
            };
            await _cardRepository.AddAsync(clonedCard);
        }

        return new DeskDto
        {
            Id = clonedDesk.Id,
            Name = clonedDesk.Name,
            IsPublic = clonedDesk.IsPublic,
            FolderId = clonedDesk.FolderId,
            CreatedAt = clonedDesk.CreatedAt,
            LastModified = clonedDesk.LastModified,
        };
    }
}

using FlashcardApi.Application.Folder;
using FlashcardApi.Application.Folder.Dtos;
using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;

namespace FlashcardApi.Infrastructure.Services;

public class FolderService : IFolderService
{
    private readonly IFolderRepository _folderRepository;

    public FolderService(IFolderRepository folderRepository)
    {
        _folderRepository = folderRepository;
    }

    public async Task<List<FolderDto>> GetUserFoldersAsync(string userId)
    {
        var folders = await _folderRepository.GetByOwnerIdAsync(userId);
        return folders
            .Select(f => new FolderDto
            {
                Id = f.Id,
                Name = f.Name,
                ParentFolderId = f.ParentFolderId,
                CreatedAt = f.CreatedAt,
                LastModified = f.LastModified,
            })
            .ToList();
    }

    public async Task<FolderDto> CreateFolderAsync(string userId, FolderDto folderDto)
    {
        var folder = new Folder
        {
            OwnerId = userId,
            Name = folderDto.Name,
            ParentFolderId = folderDto.ParentFolderId,
        };
        await _folderRepository.AddAsync(folder);
        return new FolderDto
        {
            Id = folder.Id,
            Name = folder.Name,
            ParentFolderId = folder.ParentFolderId,
            CreatedAt = folder.CreatedAt,
            LastModified = folder.LastModified,
        };
    }

    public async Task<FolderDto> UpdateFolderAsync(string id, FolderDto folderDto)
    {
        var folder = await _folderRepository.GetByIdAsync(id);
        if (folder == null)
            throw new Exception("Folder not found");

        folder.Name = folderDto.Name;
        folder.ParentFolderId = folderDto.ParentFolderId;
        folder.LastModified = DateTime.UtcNow;

        await _folderRepository.UpdateAsync(folder);
        return new FolderDto
        {
            Id = folder.Id,
            Name = folder.Name,
            ParentFolderId = folder.ParentFolderId,
            CreatedAt = folder.CreatedAt,
            LastModified = folder.LastModified,
        };
    }

    public async Task DeleteFolderAsync(string id)
    {
        var folder = await _folderRepository.GetByIdAsync(id);
        if (folder == null)
            throw new Exception("Folder not found");

        await _folderRepository.DeleteAsync(id);
    }
}


using FlashcardApi.Application.Image;
using FlashcardApi.Application.Image.Dtos;
using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;
using Microsoft.AspNetCore.Http;

namespace FlashcardApi.Infrastructure.Services;

public class ImageService : IImageService
{
    private readonly IImageRepository _imageRepository;
    private readonly string _storagePath = Path.Combine(Directory.GetCurrentDirectory(), "Uploads");

    public ImageService(IImageRepository imageRepository)
    {
        _imageRepository = imageRepository;
        if (!Directory.Exists(_storagePath))
            Directory.CreateDirectory(_storagePath);
    }

    public async Task<ImageDto> UploadImageAsync(string userId, IFormFile file, string fileName)
    {
        var filePath = Path.Combine(_storagePath, fileName);

        using (var stream = new FileStream(filePath, FileMode.Create))
        {
            await file.CopyToAsync(stream);
        }

        var image = new Image
        {
            Url = $"/Uploads/{fileName}",
            UploadedBy = userId,
        };
        await _imageRepository.AddAsync(image);

        return new ImageDto
        {
            Id = image.Id,
            FileName = fileName,
            Url = image.Url,
            UploadedAt = image.UploadedAt,
        };
    }

    public async Task DeleteImageAsync(string fileName)
    {
        var image = await _imageRepository.GetByFileNameAsync(fileName); // Cần thêm phương thức này
        if (image == null)
            throw new Exception("Image not found");

        var filePath = Path.Combine(_storagePath, fileName);
        if (File.Exists(filePath))
            File.Delete(filePath);

        await _imageRepository.DeleteAsync(image.Id);
    }
}

using FlashcardApi.Application.Interfaces;
using FlashcardApi.Application.Review.Dtos;
using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;

namespace FlashcardApi.Infrastructure.Services;

public class ReviewService : IReviewService
{
    private readonly IReviewRepository _reviewRepository;

    public ReviewService(IReviewRepository reviewRepository)
    {
        _reviewRepository = reviewRepository;
    }

    public async Task<ReviewDto> CreateReviewAsync(ReviewDto reviewDto)
    {
        var review = new Review
        {
            CardId = reviewDto.CardId,
            Ease = reviewDto.Ease,
            Interval = reviewDto.Interval,
            Repetition = reviewDto.Repetition,
            NextReviewDate = reviewDto.NextReviewDate,
            LastReviewed = reviewDto.LastReviewed,
        };
        var createdReview = await _reviewRepository.CreateAsync(review);
        return MapToDto(createdReview);
    }

    public async Task<ReviewDto> UpdateReviewAsync(string id, ReviewDto reviewDto)
    {
        var review = await _reviewRepository.GetByCardIdAsync(reviewDto.CardId);
        if (review == null || review.Id != id)
            throw new Exception("Review not found");

        review.Ease = reviewDto.Ease;
        review.Interval = reviewDto.Interval;
        review.Repetition = reviewDto.Repetition;
        review.NextReviewDate = reviewDto.NextReviewDate;
        review.LastReviewed = reviewDto.LastReviewed;

        await _reviewRepository.UpdateAsync(review);
        return MapToDto(review);
    }

    public async Task DeleteReviewAsync(string id)
    {
        await _reviewRepository.DeleteAsync(id);
    }

    public async Task<ReviewDto> GetReviewByCardIdAsync(string cardId)
    {
        var review = await _reviewRepository.GetByCardIdAsync(cardId);
        return review != null ? MapToDto(review) : null;
    }

    public async Task<List<ReviewDto>> GetReviewsDueTodayAsync(string deskId, string today)
    {
        var reviews = await _reviewRepository.GetReviewsDueTodayAsync(deskId, today);
        return reviews.Select(MapToDto).ToList();
    }

    private ReviewDto MapToDto(Review review)
    {
        return new ReviewDto
        {
            Id = review.Id,
            CardId = review.CardId,
            Ease = review.Ease,
            Interval = review.Interval,
            Repetition = review.Repetition,
            NextReviewDate = review.NextReviewDate,
            LastReviewed = review.LastReviewed,
        };
    }
}


using FlashcardApi.Application.Interfaces;
using FlashcardApi.Application.Session.Dtos;
using FlashcardApi.Domain.Entities;
using FlashcardApi.Domain.Interfaces;

namespace FlashcardApi.Infrastructure.Services;

public class SessionService : ISessionService
{
    private readonly ISessionRepository _sessionRepository;

    public SessionService(ISessionRepository sessionRepository)
    {
        _sessionRepository = sessionRepository;
    }

    public async Task<SessionDto> CreateSessionAsync(SessionDto sessionDto)
    {
        var session = new Session
        {
            DeskId = sessionDto.DeskId,
            StartTime = sessionDto.StartTime,
            EndTime = sessionDto.EndTime,
            CardsStudied = sessionDto.CardsStudied,
            Performance = sessionDto.Performance,
        };
        var createdSession = await _sessionRepository.CreateAsync(session);
        return MapToDto(createdSession);
    }

    public async Task<SessionDto> UpdateSessionAsync(string id, SessionDto sessionDto)
    {
        var session = await _sessionRepository
            .GetByDeskIdAsync(sessionDto.DeskId)
            .ContinueWith(t => t.Result.FirstOrDefault(s => s.Id == id));
        if (session == null)
            throw new Exception("Session not found");

        session.StartTime = sessionDto.StartTime;
        session.EndTime = sessionDto.EndTime;
        session.CardsStudied = sessionDto.CardsStudied;
        session.Performance = sessionDto.Performance;

        await _sessionRepository.UpdateAsync(session);
        return MapToDto(session);
    }

    public async Task DeleteSessionAsync(string id)
    {
        await _sessionRepository.DeleteAsync(id);
    }

    public async Task<List<SessionDto>> GetSessionsByDeskIdAsync(string deskId)
    {
        var sessions = await _sessionRepository.GetByDeskIdAsync(deskId);
        return sessions.Select(MapToDto).ToList();
    }

    private SessionDto MapToDto(Session session)
    {
        return new SessionDto
        {
            Id = session.Id,
            DeskId = session.DeskId,
            StartTime = session.StartTime,
            EndTime = session.EndTime,
            CardsStudied = session.CardsStudied,
            Performance = session.Performance,
        };
    }
}


using FlashcardApi.Application.ApplicationUser.Dtos;
using FlashcardApi.Application.ApplicationUser;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;
using System.Security.Claims;

namespace FlashcardApi.Presentation.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class AuthController : ControllerBase
    {
        private readonly IAuthService _authService;

        public AuthController(IAuthService authService)
        {
            _authService = authService;
        }

        [HttpPost("login")]
        public async Task<IActionResult> Login([FromBody] LoginRequestDto request)
        {
            try
            {
                var response = await _authService.LoginAsync(request);
                return Ok(response);
            }
            catch (Exception ex)
            {
                return BadRequest(new { message = ex.Message });
            }
        }


        [HttpPost("register")]
        public async Task<IActionResult> Register([FromBody] LoginRequestDto request)
        {
            try
            {
                await _authService.RegisterAsync(request.Username, request.Password);
                return Ok(new { message = "User registered successfully" });
            }
            catch (Exception ex)
            {
                return BadRequest(new { message = ex.Message });
            }
        }

        [Authorize]
        [HttpGet("me")]
        public IActionResult GetCurrentUser()
        {
            var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
            var username = User.FindFirst(ClaimTypes.Name)?.Value;
            return Ok(new { UserId = userId, Username = username });
        }

        [Authorize]
        [HttpPost("logout")]
        public async Task<IActionResult> Logout()
        {
            var token = Request.Headers["Authorization"].ToString().Replace("Bearer ", "");
            await _authService.LogoutAsync(token);
            return Ok(new { message = "Logged out successfully" });
        }
    }
}

using System.Threading.Tasks;
using FlashcardApi.Application.Card;
using FlashcardApi.Application.Card.Dtos;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace FlashcardApi.Presentation.Controllers;

[Authorize]
[Route("api/[controller]")]
[ApiController]
public class CardController : ControllerBase
{
    private readonly ICardService _cardService;

    public CardController(ICardService cardService)
    {
        _cardService = cardService;
    }

    [HttpGet]
    public async Task<IActionResult> GetCardsByDeskId([FromQuery] string deskId)
    {
        var cards = await _cardService.GetCardsByDeskIdAsync(deskId);
        return Ok(cards);
    }

    [HttpPost]
    public async Task<IActionResult> CreateCard([FromBody] CardDto cardDto)
    {
        var card = await _cardService.CreateCardAsync(cardDto);
        await _cardService.CleanupUnusedImagesAsync(cardDto.DeskId, cardDto.ImagePaths);
        return Ok(card);
    }

    [HttpPut("{id}")]
    public async Task<IActionResult> UpdateCard(string id, [FromBody] CardDto cardDto)
    {
        try
        {
            var updatedCard = await _cardService.UpdateCardAsync(id, cardDto);
            await _cardService.CleanupUnusedImagesAsync(cardDto.DeskId, cardDto.ImagePaths);
            return Ok(updatedCard);
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }

    [HttpDelete("{id}")]
    public async Task<IActionResult> DeleteCard(string id)
    {
        try
        {
            await _cardService.DeleteCardAsync(id);
            return Ok(new { message = "Card deleted successfully" });
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }
}

using System.Security.Claims;
using FlashcardApi.Application.Desk;
using FlashcardApi.Application.Desk.Dtos;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace FlashcardApi.Presentation.Controllers;

[Authorize]
[Route("api/[controller]")]
[ApiController]
public class DeskController : ControllerBase
{
    private readonly IDeskService _deskService;

    public DeskController(IDeskService deskService)
    {
        _deskService = deskService;
    }

    [HttpGet]
    public async Task<IActionResult> GetUserDesks()
    {
        var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
        var desks = await _deskService.GetUserDesksAsync(userId);
        return Ok(desks);
    }

    [HttpGet("public")]
    [AllowAnonymous]
    public async Task<IActionResult> GetPublicDesks()
    {
        var desks = await _deskService.GetPublicDesksAsync();
        return Ok(desks);
    }

    [HttpPost]
    public async Task<IActionResult> CreateDesk([FromBody] DeskDto deskDto)
    {
        var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
        var desk = await _deskService.CreateDeskAsync(userId, deskDto);
        return Ok(desk);
    }

    [HttpPut("{id}")]
    public async Task<IActionResult> UpdateDesk(string id, [FromBody] DeskDto deskDto)
    {
        try
        {
            var updatedDesk = await _deskService.UpdateDeskAsync(id, deskDto);
            return Ok(updatedDesk);
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }

    [HttpDelete("{id}")]
    public async Task<IActionResult> DeleteDesk(string id)
    {
        try
        {
            await _deskService.DeleteDeskAsync(id);
            return Ok(new { message = "Desk deleted successfully" });
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }

    [HttpPost("{id}/clone")]
    public async Task<IActionResult> CloneDesk(string id)
    {
        var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
        try
        {
            var clonedDesk = await _deskService.CloneDeskAsync(userId, id);
            return Ok(clonedDesk);
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }
}

using System.Security.Claims;
using System.Threading.Tasks;
using FlashcardApi.Application.Folder;
using FlashcardApi.Application.Folder.Dtos;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace FlashcardApi.Presentation.Controllers;

[Authorize]
[Route("api/[controller]")]
[ApiController]
public class FolderController : ControllerBase
{
    private readonly IFolderService _folderService;

    public FolderController(IFolderService folderService)
    {
        _folderService = folderService;
    }

    [HttpGet]
    public async Task<IActionResult> GetUserFolders()
    {
        var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
        var folders = await _folderService.GetUserFoldersAsync(userId);
        return Ok(folders);
    }

    [HttpPost]
    public async Task<IActionResult> CreateFolder([FromBody] FolderDto folderDto)
    {
        var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
        var folder = await _folderService.CreateFolderAsync(userId, folderDto);
        return Ok(folder);
    }

    [HttpPut("{id}")]
    public async Task<IActionResult> UpdateFolder(string id, [FromBody] FolderDto folderDto)
    {
        try
        {
            var updatedFolder = await _folderService.UpdateFolderAsync(id, folderDto);
            return Ok(updatedFolder);
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }

    [HttpDelete("{id}")]
    public async Task<IActionResult> DeleteFolder(string id)
    {
        try
        {
            await _folderService.DeleteFolderAsync(id);
            return Ok(new { message = "Folder deleted successfully" });
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }
}

using System.Security.Claims;
using System.Threading.Tasks;
using FlashcardApi.Application.Image;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;

namespace FlashcardApi.Presentation.Controllers;

[Authorize]
[Route("api/[controller]")]
[ApiController]
public class ImageController : ControllerBase
{
    private readonly IImageService _imageService;

    public ImageController(IImageService imageService)
    {
        _imageService = imageService;
    }

    [HttpPost("upload")]
    public async Task<IActionResult> UploadImage(IFormFile file, [FromQuery] string fileName)
    {
        if (file == null || file.Length == 0)
            return BadRequest(new { message = "No file uploaded" });
        if (string.IsNullOrEmpty(fileName))
            return BadRequest(new { message = "File name is required" });

        var userId = User.FindFirst(ClaimTypes.NameIdentifier)?.Value;
        var image = await _imageService.UploadImageAsync(userId, file, fileName);
        return Ok(image);
    }

    [HttpDelete]
    public async Task<IActionResult> DeleteImage([FromQuery] string fileName)
    {
        try
        {
            await _imageService.DeleteImageAsync(fileName);
            return Ok(new { message = "Image deleted successfully" });
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }
}

using FlashcardApi.Application.Interfaces;
using FlashcardApi.Application.Review.Dtos;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace FlashcardApi.Presentation.Controllers;

[Authorize]
[Route("api/[controller]")]
[ApiController]
public class ReviewController : ControllerBase
{
    private readonly IReviewService _reviewService;

    public ReviewController(IReviewService reviewService)
    {
        _reviewService = reviewService;
    }

    [HttpPost]
    public async Task<IActionResult> CreateReview([FromBody] ReviewDto reviewDto)
    {
        var review = await _reviewService.CreateReviewAsync(reviewDto);
        return Ok(review);
    }

    [HttpPut("{id}")]
    public async Task<IActionResult> UpdateReview(string id, [FromBody] ReviewDto reviewDto)
    {
        try
        {
            var updatedReview = await _reviewService.UpdateReviewAsync(id, reviewDto);
            return Ok(updatedReview);
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }

    [HttpDelete("{id}")]
    public async Task<IActionResult> DeleteReview(string id)
    {
        try
        {
            await _reviewService.DeleteReviewAsync(id);
            return Ok(new { message = "Review deleted successfully" });
        }
        catch (Exception ex)
        {
            return BadRequest(new { message = ex.Message });
        }
    }

    [HttpGet("card/{cardId}")]
    public async Task<IActionResult> GetReviewByCardId(string cardId)
    {
        var review = await _reviewService.GetReviewByCardIdAsync(cardId);
        return review != null ? Ok(review) : NotFound();
    }

    [HttpGet("due-today")]
    public async Task<IActionResult> GetReviewsDueToday(
        [FromQuery] string deskId,
        [FromQuery] string today
    )
    {
        var reviews = await _reviewService.GetReviewsDueTodayAsync(deskId, today);
        return Ok(reviews);
    }
}

using FlashcardApi.Application.Interfaces;
using FlashcardApi.Application.Session.Dtos;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;

namespace FlashcardApi.Presentation.Controllers
{
    [Authorize]
    [Route("api/[controller]")]
    [ApiController]
    public class SessionController : ControllerBase
    {
        private readonly ISessionService _sessionService;

        public SessionController(ISessionService sessionService)
        {
            _sessionService = sessionService;
        }

        [HttpPost]
        public async Task<IActionResult> CreateSession([FromBody] SessionDto sessionDto)
        {
            var session = await _sessionService.CreateSessionAsync(sessionDto);
            return Ok(session);
        }

        [HttpPut("{id}")]
        public async Task<IActionResult> UpdateSession(string id, [FromBody] SessionDto sessionDto)
        {
            try
            {
                var updatedSession = await _sessionService.UpdateSessionAsync(id, sessionDto);
                return Ok(updatedSession);
            }
            catch (Exception ex)
            {
                return BadRequest(new { message = ex.Message });
            }
        }

        [HttpDelete("{id}")]
        public async Task<IActionResult> DeleteSession(string id)
        {
            try
            {
                await _sessionService.DeleteSessionAsync(id);
                return Ok(new { message = "Session deleted successfully" });
            }
            catch (Exception ex)
            {
                return BadRequest(new { message = ex.Message });
            }
        }

        [HttpGet("desk/{deskId}")]
        public async Task<IActionResult> GetSessionsByDeskId(string deskId)
        {
            var sessions = await _sessionService.GetSessionsByDeskIdAsync(deskId);
            return Ok(sessions);
        }
    }
}










